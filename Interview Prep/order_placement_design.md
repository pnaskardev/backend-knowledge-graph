# Order Placement Design — Kirana Club

**The prompt:** "Design order placement for a B2B commerce platform where kirana retailers order from distributors."

**How to use this:** read it once start to finish (15 minutes). Then close it and redraw sections 3, 4 and 5 on paper from memory. That is the whole exercise.

**A note on the numbers:** the traffic figures are my estimates, not Kirana Club's real numbers. In the interview, say them as assumptions and ask the interviewer to correct you.

---

## 1. Ask first (2–3 minutes)

Before drawing anything, ask these. Each one changes the design.

| Question | Why it matters |
|---|---|
| How many orders a day, and what's the peak? | Decides whether you need anything fancy at all |
| One distributor per order, or can one order split across several? | Splitting makes it much harder, so start with one |
| Pay upfront or on credit? | Credit means a credit-limit check, which is a second race condition |
| Can a distributor supply only part of an order? | In B2B, yes. It changes the data model |
| Is there an existing system, or is this greenfield? | Decides whether you're designing or extending |

For the rest of this doc, assume: **about 80,000 orders a day, one distributor per order, mostly credit, partial fulfilment possible, greenfield.**

## 2. Do the math out loud (2 minutes)

- 80,000 orders a day ÷ 86,400 seconds ≈ **1 order per second** on average.
- Peak is maybe 10x, so about **10 orders a second**.
- Each order has about 10 line items, and one order is about 1 KB. That's under 1 GB a day, roughly **300 GB a year**.
- Reads are much bigger: browsing the catalog is about **60x** the number of orders.

**Conclusion to say out loud:**

> "The order write path is a small number. One Postgres primary handles it with a lot of room. So this isn't a scaling problem, it's a correctness problem. I'll keep it simple and make it strictly correct, and spend my scaling effort on the read side."

That paragraph is worth more than any diagram.

## 3. The picture

```
 Retailer's phone
        │  POST /orders  (Idempotency-Key: abc-123)
        ▼
 ┌───────────────┐
 │  API gateway  │  auth, rate limit
 └───────┬───────┘
         ▼
 ┌───────────────────────────────────────────────┐
 │  Order service                                │
 │                                               │
 │   ONE Postgres transaction:                   │
 │   1. idempotency row  (unique key decides)    │
 │   2. re-price from source of truth            │
 │   3. credit check     (conditional update)    │
 │   4. reserve stock    (conditional update)    │
 │   5. insert order + lines (prices frozen)     │
 │   6. insert outbox row                        │
 │   7. COMMIT                                   │
 └───────────────────────┬───────────────────────┘
                         │  201 Created  → back to the phone
                         ▼
                  outbox relay (separate process)
                         │  publishes OrderPlaced
         ┌───────────────┼────────────────┐
         ▼               ▼                ▼
    Notification    Distributor       Analytics
    (SMS / push)    adapter           (reporting)
                         │
                         ▼
              distributor confirms / rejects / partial
                         │
                         ▼
              order state machine updates
```

Two things to point at:

- **Everything inside the box is one database transaction.** If any step fails, all of it is undone automatically.
- **Everything below the box is async.** None of it is allowed to fail the order.

## 4. The data model

This is where you slow down. A correct data model makes the rest obvious.

```sql
-- One row per attempt to place an order. The unique key is the dedup mechanism.
CREATE TABLE idempotency_keys (
  retailer_id    bigint      NOT NULL,
  key            text        NOT NULL,
  request_hash   text        NOT NULL,   -- catches "same key, different body"
  status         text        NOT NULL,   -- in_progress | done
  order_id       uuid,
  response_body  jsonb,                  -- stored so a duplicate gets the SAME answer
  created_at     timestamptz NOT NULL DEFAULT now(),
  PRIMARY KEY (retailer_id, key)
);

CREATE TABLE orders (
  id             uuid        PRIMARY KEY,        -- UUID v7: time-ordered, index-friendly
  retailer_id    bigint      NOT NULL,
  distributor_id bigint      NOT NULL,
  status         text        NOT NULL,           -- see state machine in section 7
  total_paise    bigint      NOT NULL,           -- integer paise, never floats
  created_at     timestamptz NOT NULL DEFAULT now()
);
CREATE INDEX ON orders (retailer_id, created_at DESC);   -- "my orders" screen

CREATE TABLE order_lines (
  order_id          uuid   NOT NULL REFERENCES orders(id),
  sku_id            bigint NOT NULL,
  qty_ordered       int    NOT NULL,
  qty_confirmed     int,                 -- what the distributor agreed to supply
  qty_delivered     int,                 -- what actually arrived
  unit_price_paise  bigint NOT NULL,     -- FROZEN at order time
  PRIMARY KEY (order_id, sku_id)
);

CREATE TABLE inventory (
  sku_id         bigint NOT NULL,
  distributor_id bigint NOT NULL,
  on_hand        int    NOT NULL,
  reserved       int    NOT NULL DEFAULT 0,
  PRIMARY KEY (sku_id, distributor_id),
  CHECK (on_hand - reserved >= 0)        -- the backstop: stock can never go negative
);

CREATE TABLE reservations (
  id             uuid PRIMARY KEY,
  order_id       uuid NOT NULL REFERENCES orders(id),
  sku_id         bigint NOT NULL,
  distributor_id bigint NOT NULL,
  qty            int NOT NULL,
  status         text NOT NULL,          -- active | committed | released
  expires_at     timestamptz NOT NULL
);

CREATE TABLE retailer_credit (
  retailer_id      bigint PRIMARY KEY,
  limit_paise      bigint NOT NULL,
  outstanding_paise bigint NOT NULL DEFAULT 0,
  reserved_paise   bigint NOT NULL DEFAULT 0,
  CHECK (outstanding_paise + reserved_paise <= limit_paise)
);

CREATE TABLE outbox (
  id          bigserial   PRIMARY KEY,
  event_type  text        NOT NULL,
  payload     jsonb       NOT NULL,
  created_at  timestamptz NOT NULL DEFAULT now(),
  sent_at     timestamptz              -- NULL means not published yet
);
CREATE INDEX ON outbox (id) WHERE sent_at IS NULL;   -- tiny partial index
```

**Four choices to explain if asked:**

1. **`unit_price_paise` lives on the order line.** Store the price it was placed at, not a pointer to a price that can change. Otherwise an old order shows today's price and your accounting is wrong forever.
2. **Three quantity columns.** Ordered, confirmed, delivered. Partial fulfilment is normal in B2B, so it's a real state, not an error.
3. **`CHECK` constraints on stock and credit.** The conditional update is the good behaviour. The constraint is the guarantee for the code path someone writes next year and forgets.
4. **Money is integer paise.** 0.1 can't be stored exactly in floating point, and those errors pile up into reconciliation breaks.

## 5. The transaction, step by step

This is the heart of the answer. Say it slowly.

**Step 1: claim the idempotency key.**

```sql
INSERT INTO idempotency_keys (retailer_id, key, request_hash, status)
VALUES (:retailer, :key, :hash, 'in_progress')
ON CONFLICT DO NOTHING;
```

- 1 row inserted: you own this request, carry on.
- 0 rows inserted: someone already has this key. If their status is `done`, **return their stored response**. If it's `in_progress`, return `409` so the client retries shortly.
- Same key but a different `request_hash`: reject. That's a client bug.

The database's unique constraint decides the winner. Never "check if it exists, then insert". That's a race, and two pods can both pass the check in the same millisecond.

**Step 2: re-price from the source of truth.**

Never trust a price the client sent. Look up the price list for this retailer's segment, apply volume slabs and promotions, compute the total. If it differs from what the app displayed beyond a small tolerance, return the new price and ask the retailer to confirm. Never silently charge a different price.

**Step 3: check credit with a conditional update.**

```sql
UPDATE retailer_credit
SET reserved_paise = reserved_paise + :total
WHERE retailer_id = :retailer
  AND limit_paise - outstanding_paise - reserved_paise >= :total;
```

It affects one row or zero. Zero means over the limit. This is not "read the balance, check it in code, then write", because two concurrent orders could both pass a limit they jointly exceed.

**Step 4: reserve stock with a conditional update.**

```sql
UPDATE inventory
SET reserved = reserved + :qty
WHERE sku_id = :sku AND distributor_id = :dist
  AND on_hand - reserved >= :qty;
```

Same shape: one row or zero. Process the lines **sorted by `sku_id`**. Every transaction locks rows in the same order, so two orders can't deadlock each other.

**Step 5: insert the order, the lines and the reservations.** Prices frozen onto the lines. Reservation expiry set (say 30 minutes if payment is pending, none needed for approved credit).

**Step 6: insert the outbox row** for `OrderPlaced`, in the same transaction.

**Step 7: save the response on the idempotency row and COMMIT.**

**If anything fails anywhere, the transaction rolls back and the credit reservation, stock reservation and order row all vanish together.** That's the reason to keep this in one database: there's nothing to compensate. A rollback is free and always correct.

### What deliberately stays outside the transaction

- Calling a payment gateway.
- Calling the distributor's API.
- Sending SMS or push.
- Writing analytics.

**Never make a network call to a third party inside a database transaction.** If their API hangs for 30 seconds, you've held row locks for 30 seconds and everything queueing behind those rows backs up.

## 6. After the commit: the async part

A separate **relay** process reads unsent outbox rows and publishes them:

```sql
SELECT * FROM outbox
WHERE sent_at IS NULL
ORDER BY id
LIMIT 100
FOR UPDATE SKIP LOCKED;
```

`SKIP LOCKED` means several relay instances can run at once and each grabs different rows without waiting on each other.

The relay publishes, then marks `sent_at`. If it crashes between those two steps, the event goes out twice. That's fine, because **consumers are idempotent and dedupe on event ID.** At-least-once delivery plus idempotent consumers gives you effectively-once processing. Exactly-once across a network doesn't exist.

Consumers of `OrderPlaced`:

| Consumer | Does | Failure effect |
|---|---|---|
| Notification | SMS or push to retailer and distributor | None on the order |
| Distributor adapter | Sends the order to the distributor in whatever form they accept | Retried, circuit-broken, reconciled |
| Analytics | Writes to reporting | None on the order |

**At one order a second, you don't need Kafka for this.** A Postgres table plus `SKIP LOCKED` is enough. Say so, and name the trigger: several independent teams consuming the same events, or wanting replay.

## 7. The order state machine

```
 placed ──► confirmed ──► dispatched ──► delivered
    │           │
    │           └──► partially_confirmed ──► dispatched ──► delivered
    │
    ├──► rejected   (distributor declined everything)
    └──► cancelled  (retailer cancelled before dispatch)
```

Rules:

- **Transitions are checked and one-directional.** A late "confirmed" message can't move a `dispatched` order backwards. It's rejected, not applied. That one rule handles out-of-order messages.
- **Write transitions as conditional updates:** `UPDATE orders SET status='confirmed' WHERE id=:id AND status='placed'`. If another transition got there first, you get zero rows and lose cleanly.
- **Cancelling is cheap before dispatch and expensive after.** Dispatch is the point of no return, so put anything that might cancel the order (fraud checks, credit review) *before* it.

When a distributor rejects or short-ships:

- Release the reservation: `reserved = reserved - qty`, using an increment, not a "set to the number I remembered".
- Reduce `reserved_paise` on the retailer's credit by the unfulfilled amount.
- Set `qty_confirmed` per line, move to `partially_confirmed` or `rejected`, notify the retailer.

These are just updates in a local database, so they're simple and idempotent.

## 8. What breaks, and what happens

Spend real time here in the interview. Most people run out of clock before reaching it.

| Failure | What happens |
|---|---|
| **Two pods get the same request in the same millisecond** | The unique constraint on the idempotency key lets one in. The other gets the stored response or a 409. One order. |
| **Phone loses connection right after tapping, app retries** | Same key, finds the finished row, returns the stored response. One order, no matter how many taps. |
| **Two retailers want the last 5 cases** | The conditional update affects one row or zero. The loser gets a clean "insufficient stock". Stock never goes negative. |
| **Two orders race on a retailer's credit limit** | Same pattern. One passes, one fails cleanly. |
| **Crash in the middle of the transaction** | Postgres rolls back everything. No half-order exists. |
| **Crash after commit, before the relay publishes** | The outbox row is already committed, so the relay publishes it when it restarts. No lost event. |
| **Relay publishes, then crashes before marking sent** | The event is published twice. Consumers dedupe on event ID. |
| **Distributor's API is down** | Per-partner timeout, retry with backoff and jitter, circuit breaker so it fails fast. The order is already safely placed. Work is queued and retried. |
| **Distributor confirms only half** | State moves to `partially_confirmed`, reservation and credit released for the missing part, retailer notified. |
| **A late or duplicate webhook from the distributor** | State machine rejects illegal backwards moves. Event ID dedupe handles duplicates. |
| **The job that releases expired reservations dies** | Stock stays locked and nobody notices, which is the sneaky one. That job needs a metric and an alert on reservations older than their expiry. |
| **Price changed between browsing and ordering** | Re-priced at order time. If it moved beyond tolerance, show the new price and ask. Never silently charge more. |

## 9. Scaling it (only after the above)

Scale the read side, not the write side.

| Lever | What | Cost to name |
|---|---|---|
| **Index on `(retailer_id, created_at DESC)`** | "My orders" is a few milliseconds | Slightly slower writes |
| **Read replicas** | Move order history and catalog reads off the primary | Replication lag. Route a retailer's reads to the primary for a few seconds after they order, or they won't see their own order |
| **Cache the catalog and price lists** | Resolved price list per retailer segment, short TTL | Staleness. **Never cache the stock count you commit against** |
| **Partition `orders` by month** | Faster scans, cheap archival | Queries without a date hit every partition |
| **PgBouncer** | Many app containers share few real connections | Session-level features break |

**Deliberately not building:**

- **Sharding.** One primary handles this for years. It's a one-way door that costs cross-shard joins and transactions. The trigger would be the write rate approaching what one primary can take, or the data outgrowing one machine's disk.
- **Kafka.** Not at one order a second. The trigger is several teams consuming the same stream, or wanting replay.
- **A saga.** Order, credit and inventory live in one database, so a single transaction beats any saga. The trigger for needing one is splitting them into separate services, and I'd want a strong reason before doing that.
- **Microservices.** Start as a modular monolith with clear internal boundaries.

## 10. If they change the requirements

**"Orders can now span several distributors."**

The single transaction still works if everything is in one database, but the distributors confirm independently. So split the basket into one **child order per distributor** under a parent. Each child has its own state machine and reservation. The hard part is what the retailer sees when one child is rejected and two are confirmed. That's a product decision (partial delivery, wait for all, or cancel all), so ask rather than assume.

**"Inventory is now owned by a separate service."**

Now you've lost the single transaction and you need a saga: reserve stock → reserve credit → create order, with compensations in reverse. Order the steps so reversible ones come first. Make every compensation idempotent. Treat a failed compensation as a page, not a dead letter. And say that you'd have pushed back on the split.

**"10x the traffic."**

800,000 orders a day is about 10 writes a second average. One primary still handles that. The first thing to break is the catalog and price read path, which is why that's what's been designed to scale.

## 11. The 30-minute run

| Minutes | Do |
|---|---|
| 0–3 | Ask the clarifying questions |
| 3–5 | Math out loud, conclude it's a correctness problem |
| 5–8 | Entities and API (`POST /orders`, `GET /orders`, `GET /orders/{id}`, `POST /orders/{id}/cancel`) |
| 8–15 | Data model. Slow down. Draw the tables |
| 15–20 | The transaction, step by step. Point out what stays outside |
| 20–28 | Failure modes. Use the table in section 8 |
| 28–30 | Scaling and what you chose not to build, each with a trigger |

## 12. The six sentences to have ready

1. **"This is about one write a second, so it's a correctness problem, not a scaling problem."**
2. **"The database's unique constraint decides the winner, not my application code."**
3. **"A conditional update that affects one row or zero, never read-then-check-then-write."**
4. **"Prices are frozen onto the order line, and stock is never cached at the point of commitment."**
5. **"No third-party network calls inside the transaction, and the outbox makes the event and the order agree."**
6. **"I wouldn't shard, add Kafka or write a saga yet. Here's the number that would change my mind."**

If you can say those six and draw the data model, you have the core of this answer.
