# Kirana Club — Round 2 | Scaling a B2B Commerce Platform

**Role:** Software Engineer — Backend (SDE 2), Bangalore
**What gets tested:** resume · technical depth · business problems · problem decomposition · product and business sense · prioritisation and tech judgement
**Companion doc:** `kirana_club.md` (Round 1 — fundamentals, your stories, the resume cross-examination in Appendix A)

---

## How to read this

Round 1 was "do you know your fundamentals and did you really build what your resume says." Round 2 is different. It's **"can you design a system you've never built, for a business you've just learned about, and explain why your choices are the right ones."**

That means the answers are longer, messier, and more about judgement than recall. There is no single right design. There are good trade-offs stated clearly and bad ones stated confidently.

Every topic below follows the same shape, so you can drill it:

- **What it is** — in plain words
- **An example** — usually a kirana store buying Parle-G, so it stays concrete
- **Pros and cons** — because the interview scores the cons more than the pros
- **When to use it, when not to**
- **The interview line** — the one sentence to actually say out loud

Read Parts 0–2 first. They change how you answer everything else. Then work through Part 5, which is the actual meat — the subsystems of a commerce platform. Part 12 has three fully worked mock answers; do those last, out loud, with a timer.

---

# Part 0 — What this round actually is

## 0.1 The six things they're scoring

They told you the axes. That's a gift — most companies don't. Here's what each one actually means in practice, and what a good answer looks like.

| Axis | What they're really asking | What a bad answer looks like | What a good answer looks like |
|---|---|---|---|
| **Resume** | Did you build it, and can you now generalise from it? | Repeating the bullet points | "I solved this exact problem at Kazam, here's how it maps to your case, and here's what's different" |
| **Technical depth** | Do you know how the thing actually works underneath? | Naming technologies | Naming the mechanism — "the unique constraint arbitrates, not the application code" |
| **Business problems** | Can you turn a business goal into a system? | Jumping to architecture | "Before I design, what's the metric we're moving and what's the current number?" |
| **Problem decomposition** | Can you split a vague mess into pieces? | One giant undifferentiated design | "There are four sub-problems here. Three are easy, one is hard. Let me do the hard one first." |
| **Product and business sense** | Do you understand *why* this product exists? | Designing for Amazon when they're not Amazon | "Your users are on 3G with low-end phones, so the payload budget drives the API design" |
| **Prioritisation and tech judgement** | Do you know what NOT to build? | Designing the maximum system | "At your current scale you don't need to shard. Here's the number that would change my mind." |

**The single highest-scoring behaviour across all six is saying what you would *not* do, and why.** Most candidates demonstrate knowledge by adding things. Senior engineers demonstrate it by removing things and naming the threshold at which they'd add them back.

## 0.2 The format to expect

A round like this usually runs 45–60 minutes and goes roughly: a few minutes on your background and one resume deep-dive, then one large open-ended design or business prompt that takes up the bulk, with the interviewer steering into whichever of the six axes you haven't shown yet. Expect them to change the requirements halfway through on purpose — that's the "ambiguity and changing requirements" line from the JD being tested live.

**When they change the requirement, do not defend your old design.** Say what breaks, what survives, and what it costs to adapt. That's the whole point of the exercise.

## 0.3 The four sentence patterns that carry this round

Memorise these. They're the difference between knowing things and sounding senior.

1. **"I chose X over Y because Z, and the cost is W."** Every design decision. No exceptions.
2. **"At this scale, I wouldn't build that yet. I'd build it when [specific number]."** This is the prioritisation axis in one sentence.
3. **"Let me check my assumption — is it [X] or [Y]? Because the design changes."** Shows you know which unknowns actually matter.
4. **"That breaks when [specific scenario]. The fix is [specific thing], and the cost is [specific cost]."** This is how you volunteer the weakness of your own design before they find it.

---

# Part 1 — How to run a design question

## 1.1 The method, in order

Most candidates fail design rounds on process, not knowledge. They start drawing boxes in minute two and run out of time before failure modes. Use this order every single time.

**Step 1 — Clarify scope and scale. (3–5 min)**

Ask before you build. The questions that actually change the design:

- How many users, and how many are active daily? (registered vs active is usually a 10–40x difference)
- How many orders a day? How many catalog reads per order?
- What's the read-to-write ratio?
- What's the peak-to-average traffic ratio? When is peak?
- What's explicitly out of scope?
- Is there an existing system I'm extending, or is this greenfield?

**This step is scored.** Jumping straight to architecture is the most common failure in the whole round. And asking "what's the peak-to-average ratio" marks you immediately, because almost nobody asks it and it's the number that decides whether you need a queue.

**Step 2 — Do the back-of-envelope math. (2–3 min)**

Turn the answers into requests per second, gigabytes per year, and rows per table. Out loud. Part 2 teaches you how. This single step does more for your score than any technology choice, because it's what lets you say "you don't need that yet" with authority instead of as an opinion.

**Step 3 — Define the API surface and core entities. (3–5 min)**

What are the five to eight nouns in this system, and what are the main endpoints? Keep it tiny. `POST /orders`, `GET /catalog`, `POST /payments`. Naming the entities forces the domain to become clear and it stops you designing infrastructure for a domain you haven't defined.

**Step 4 — Design the data model. (5–8 min — slow down here)**

This is your strongest ground. Tables, keys, the one or two indexes that matter, and which constraint enforces which business rule. **A correct data model makes most of the rest of the design obvious.** It's also the part most candidates rush and most interviewers care about.

**Step 5 — Walk the happy path end to end. (5 min)**

One request, one complete journey. "The retailer taps Place Order. The app sends a POST with an idempotency key. The API validates, checks credit, reserves inventory in one transaction, writes the order row and an outbox row, commits, returns 201. The relay publishes OrderPlaced. The notification service sends an SMS. The distributor service pushes it to the distributor's system."

**Step 6 — Failure modes and trade-offs. (8–10 min — budget for this deliberately)**

What happens when the payment gateway times out? When the distributor's API is down? When two retailers order the last unit at the same time? When a deploy goes out mid-order? **Almost everyone runs out of clock before this section, so getting here at all puts you ahead.** Set a mental alarm: if you're 60% through the time and haven't started failure modes, cut the design short and move.

**Step 7 — Scaling levers. (3–5 min)**

Only now. Cache, read replicas, partition, make it async, shard. And for each, say what it costs and at what number you'd reach for it.

## 1.2 Things that lose points

- **Designing for a scale nobody asked for.** If they say 10,000 orders a day and you propose Kafka, Cassandra, and a service mesh, you've failed the judgement axis even if every component is correct.
- **Naming technologies instead of mechanisms.** "I'd use Redis" is worth nothing. "I'd cache the resolved price list per retailer segment with a 5-minute TTL, because prices change on a daily cycle and a 5-minute staleness window is acceptable to the business" is worth everything.
- **Silence while thinking.** Narrate. "I'm weighing whether to put this in the same transaction or make it async — let me think about what happens if it fails."
- **Not asking what the business actually needs.** Designing a perfect system for the wrong problem.
- **Refusing to commit.** After naming a trade-off, pick one. "Both are valid, I'd go with X because of Z" beats "it depends" every time.

## 1.3 When they change the requirements mid-answer

They will. Something like "actually, now assume distributors can also sell to each other" or "now we're doing this in 4 languages" or "what if a single brand runs a flash sale."

The script:

1. "Okay, let me think about what that breaks." (Pause. Actually think.)
2. Name what still works. "The order and payment path is unaffected because..."
3. Name what breaks. "The pricing model breaks, because I assumed one price list per retailer segment and now I need..."
4. Give the cheapest fix and the proper fix, with the difference between them. "The quick version is X, which gets us there in a week but has limitation Y. The proper version is Z, which is a month. Given this is probably an experiment, I'd ship X with a flag."

That last move — offering a cheap version and a proper version, and recommending one based on how certain the business is — hits the prioritisation axis directly.

---

# Part 2 — Scale, in actual numbers

This is the part that separates people who have read system design blogs from people who can engineer. **Learn to do this arithmetic out loud in under two minutes.**

## 2.1 Why the math matters more than the architecture

Because almost every "scalable architecture" is unnecessary at the scale you're actually at, and the interviewer knows it. If you can show the numbers and conclude "a single well-indexed Postgres handles this with room to spare," you have demonstrated more seniority than any diagram.

## 2.2 The numbers you need in your head

| Thing                        | Rough number                                                           |
| ---------------------------- | ---------------------------------------------------------------------- |
| Seconds in a day             | ~86,400 — call it **100,000** for mental math                          |
| 1 million/day                | ~**12 per second** average                                             |
| 10 million/day               | ~**120 per second**                                                    |
| Typical peak-to-average      | **3–10x**, higher for a flash sale                                     |
| Postgres on decent hardware  | thousands of simple reads/sec, hundreds to low thousands of writes/sec |
| Redis                        | ~100,000 ops/sec, single-threaded                                      |
| One row of order data        | ~1 KB with line items                                                  |
| Disk is cheap, memory is not | 1 TB of disk ≈ trivial; 1 TB of RAM ≈ expensive                        |
| Network call                 | ~1–10 ms same region; disk seek ~1 ms SSD; RAM ~100 ns                 |

## 2.3 Working the Kirana Club numbers out loud

Nobody has given you these, so **state them as assumptions and invite correction.** That itself is scored.

> "Let me size this. You've got around 4 million registered retailers. Registered isn't active, so let me assume 10% monthly active — that's 400,000 — and maybe 100,000 daily active. Stop me if that's way off."

> "A retailer probably restocks once or twice a week, not daily. So say 2% of the registered base orders on a given day — around 80,000 orders a day. That's **roughly one order per second on average**. Even at a 10x peak that's 10 orders a second. That is a very small write rate."

> "Reads are the opposite. 100,000 daily active users browsing a catalog, maybe 50 screen loads each — that's 5 million reads a day, around **60 per second average, maybe 500 at peak**. So this is a read-heavy system with a roughly 60:1 read-to-write ratio."

> "Storage: 80,000 orders a day × 10 line items × roughly 1 KB is under a gigabyte a day. Call it **300 GB a year** including indexes. That fits on one machine for years."

**Then the conclusion, which is the whole point:**

> "So the honest answer is that the order write path is not a scaling problem at all — one Postgres primary handles it with a lot of headroom. The scaling problems here are the read path, the catalog and pricing fan-out, and the feed. That's where I'd spend the design effort."

That paragraph is worth more than a perfect microservice diagram. It shows you size before you build.

## 2.4 Read-heavy versus write-heavy — why it's the first question

Almost every scaling decision falls out of this one ratio.

**Read-heavy systems** (catalog, feed, product pages, search) scale with **caching, read replicas, denormalised read models, and CDNs**. These are cheap, well-understood, and mostly don't risk correctness, because a stale read is usually survivable.

**Write-heavy systems** (order placement, inventory decrement, ledger entries) scale with **partitioning, batching, making work async, and reducing contention**. These are expensive and risk correctness, because a lost or duplicated write is a real business problem.

**The interview line:** *"This is read-heavy at roughly 60:1, so I'd optimise reads with caching and a denormalised read model, and keep the write path simple and strictly correct. Writes aren't the bottleneck here, correctness on writes is the requirement."*

## 2.5 Vertical vs horizontal scaling

**Vertical** means a bigger machine. **Horizontal** means more machines.

**Example.** Your Postgres is at 80% CPU. Vertical: move from a 4-core to a 16-core box, half an hour of downtime, done. Horizontal: shard the database across four machines, three months of work, and every cross-shard query becomes a problem.

|                | Pros                                                                                          | Cons                                                                                                                                |
| -------------- | --------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **Vertical**   | Trivially simple. No code changes. Instant. Keeps transactions, joins and constraints intact. | Has a ceiling. Usually means downtime to resize. One machine is one failure domain. Cost rises faster than linearly at the top end. |
| **Horizontal** | No ceiling. Can be cheaper per unit. Failure of one node isn't fatal.                         | Much more complexity. Lose cross-node transactions and joins. Rebalancing is painful. Needs real operational maturity.              |
|                |                                                                                               |                                                                                                                                     |

**When to use which:** vertical first, always, for databases. Horizontal first for stateless application servers, where it's nearly free.

**The interview line:** *"I'd scale the database vertically until it genuinely can't go further, because vertical scaling buys you years for a day of work, and sharding is a one-way door. The app servers I'd scale horizontally from day one since they're stateless."*

## 2.6 Stateless services — the rule that makes horizontal scaling possible

**What it is.** A service is stateless when any instance can handle any request, because nothing important is stored in that instance's memory.

**Example of getting it wrong.** You keep a rate-limiter counter in a Node.js variable. You run three containers. Your "100 requests per minute" limit is now effectively 300, and it changes every time you deploy. Same bug shape: in-memory caches that go stale differently per instance, WebSocket connection maps, in-memory session stores.

**The fix.** Push shared state into Redis or the database. Keep only per-request state in memory.

| Pros | Cons |
|---|---|
| Any instance serves any request, so load balancing is trivial | Every piece of shared state becomes a network call |
| Deploys and autoscaling become safe | You now depend on Redis being up |
| An instance dying costs you nothing | Slightly higher latency per request |

**The interview line:** *"Services stay stateless so I can add and remove instances freely. Anything shared — rate limits, sessions, caches, locks — lives in Redis, not in process memory."*

## 2.7 The only four scaling levers that exist

Everything in this document is one of these four. If you remember nothing else, remember this list, because you can derive most designs from it.

1. **Do it less often** — caching, CDN, batching, deduplication.
2. **Do it somewhere else** — read replicas, async queues, background jobs, pushing work to the client.
3. **Do it in parallel** — more stateless instances, partitioning, sharding, consumer groups.
4. **Do less of it** — pagination, trimming payloads, lazy loading, sampling, saying no to the feature.

**The interview line:** *"Before adding infrastructure I ask whether I can just do it less often or do less of it. Those are free. Parallelism is the expensive one, so it's last."*

---

# Part 3 — The data layer

This is where commerce systems live or die, and it's your strongest ground. Go slow here in the interview.

## 3.1 SQL or NoSQL for a commerce platform

**The short answer: SQL, and you should be able to defend it hard.**

**Why.** Commerce is full of rules that must never be broken. An order total must equal the sum of its line items. Stock can't go negative. A payment must map to exactly one order. These are *constraints*, and a relational database enforces constraints for you, in one place, no matter which service or script or intern writes the row. In a document database you enforce them in application code, which means you enforce them in every piece of application code, forever.

**Example.** Retailer orders 10 cases of Parle-G. In Postgres: one transaction decrements inventory, inserts the order, inserts the line items, writes the ledger entry. Either all of it happens or none of it does. In MongoDB without a transaction, you can end up with stock decremented and no order — free product, unhappy accountant.

|                                     | Pros                                                                                                                                                     | Cons                                                                                                                                        |
| ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **Relational (Postgres)**           | ACID transactions. Constraints enforced by the DB. Joins. Mature tooling. Flexible querying as requirements change. `jsonb` covers semi-structured data. | Harder to shard. Schema migrations need care. One primary for writes.                                                                       |
| **Document (Mongo)**                | Flexible schema. Sharding built in. Good for genuinely variable documents.                                                                               | You enforce correctness in app code. Cross-document transactions are awkward. Easy to end up with five different shapes of the same entity. |
| **Key-value (Redis, DynamoDB)**     | Extremely fast and predictable at scale.                                                                                                                 | No querying beyond the key. No relationships.                                                                                               |
| **Search (Elasticsearch)**          | Fantastic full-text and faceted search.                                                                                                                  | Not a source of truth. Eventually consistent. Operationally heavy.                                                                          |
| **Columnar (ClickHouse, BigQuery)** | Analytics over billions of rows.                                                                                                                         | Terrible for single-row operations.                                                                                                         |

**The mature position, and the one to say:** *"Postgres as the source of truth for anything with money or stock in it, because I want the database enforcing the invariants. Then purpose-built stores alongside it for the things Postgres is bad at — Elasticsearch for search, Redis for hot reads, a columnar store for analytics. Those are all derived data, so if they're stale or lost I can rebuild them from Postgres."*

**That last clause is the key idea: one source of truth, many derived read stores.** It's the organising principle of every large commerce backend.

## 3.2 Indexing — the cheapest performance win there is

**What it is.** An index is a sorted lookup structure so the database doesn't read every row. Without one, finding one order among 30 million means reading 30 million rows.

**Example.** `SELECT * FROM orders WHERE retailer_id = 4821 ORDER BY created_at DESC LIMIT 20`. Without an index: full table scan, seconds. With an index on `(retailer_id, created_at DESC)`: a few milliseconds, and the sort is free because the index is already in that order.

Things to know and say:

- **Composite index order matters.** `(retailer_id, status, created_at)` serves a filter on `retailer_id`, or `retailer_id + status`, or all three — but **not** `status` alone. Leftmost prefix.
- **Partial indexes** for skewed columns: `CREATE INDEX ... WHERE status = 'pending'` is tiny when 99% of orders are `completed`.
- **Covering indexes** (`INCLUDE`) let the DB answer from the index alone, never touching the table.
- **Indexes cost writes.** Every insert updates every index. An over-indexed table is slow to write.

| Pros | Cons |
|---|---|
| Massive read speedup, often 1000x | Slows every write |
| Cheap to add | Uses disk and memory |
| No application changes | A wrong index is dead weight nobody notices |

**The interview line:** *"Before I reach for a cache I check the index, because a missing index is usually the actual problem and an index is free compared to the consistency cost of a cache."*

That sentence scores well because most candidates reach for Redis immediately.

## 3.3 Read replicas

**What it is.** Copies of your database that receive a stream of changes from the primary. Writes go to the primary; reads can go to any replica.

**Example.** Catalog browsing at 500 reads/sec is killing your primary, which also has to handle order writes. Add two replicas, point all catalog reads at them, and the primary is now doing almost nothing but writes.

**The catch you must name: replication lag.** A replica is usually milliseconds behind, but under load it can be seconds. So:

> Retailer places an order → write goes to the primary → app immediately redirects to "My Orders" → that read goes to a replica that hasn't caught up → **the order isn't there.** The retailer panics and orders again.

This is called the **read-your-writes** problem and it's the single most common replica bug. Fixes: route reads to the primary for a few seconds after that user writes; or pin that user's session to the primary briefly; or return the created object in the write response so the UI doesn't need to re-read.

| Pros                                  | Cons                                    |
| ------------------------------------- | --------------------------------------- |
| Scales reads almost linearly, cheaply | Replication lag causes stale reads      |
| No application rewrite needed         | Doesn't help write throughput at all    |
| Replica doubles as a failover target  | More infrastructure to run and monitor  |
| Heavy analytics can run off a replica | Easy to introduce read-your-writes bugs |

**When to use:** read-heavy workloads — which this one is. **When not to:** anything that needs to read its own write immediately, and anything write-bound.

**The interview line:** *"Read replicas are the first read-scaling lever because they're cheap and need no rewrite. The thing I'd be careful about is read-your-writes — a retailer who just placed an order must see it, so that specific read goes to the primary for a short window after the write."*

## 3.4 Caching

**What it is.** Keep a copy of an expensive answer somewhere fast, so you don't recompute it.

**Example.** Resolving the price a specific retailer sees for a specific SKU means checking their tier, their region, active promotions and which distributor serves them — maybe four queries. Do that for 40 items on a catalog screen and it's 160 queries per screen load. Cache the resolved price list per **retailer segment** (not per retailer — that's a huge number of keys) with a short TTL, and it becomes one lookup.

**The patterns.** *Cache-aside* (app checks cache, misses, reads DB, fills cache) is the default. *Write-through* (write both together) keeps them consistent at the cost of write latency. *Write-behind* (write cache, flush to DB later) is fastest and can lose data.

**The hard part is invalidation, and you should say so unprompted.** A cached price that's wrong is worse than a slow price. The three honest options:

1. **TTL only.** Simple, and you accept staleness up to the TTL. *Perfectly acceptable if you name the window* — "prices change on a daily cycle so a 5-minute TTL is fine."
2. **Delete on write.** Tighter, but has a race: a reader can fetch the old value from the DB and write it into the cache *after* the writer deleted the key, resurrecting stale data forever. Fix with a short TTL as a backstop.
3. **Versioned keys.** Put a version or `updated_at` in the key, so a write just creates a new key and the old one ages out. No invalidation race at all. Costs memory.

**Cache stampede** is the other failure. A hot key expires and a thousand requests all miss at once and all hit the database together, which falls over. Fixes: jittered TTLs so keys don't expire in lockstep; a single-flight lock so one request recomputes while the rest wait; or serve the stale value while one worker refreshes it.

| Pros | Cons |
|---|---|
| Huge latency and load reduction | Introduces a second source of truth that can lie |
| Cheap compared to scaling the DB | Invalidation is genuinely hard |
| Absorbs traffic spikes | Cold start after deploy or eviction can take down the DB |
| | Hides problems instead of fixing them |

**The interview line:** *"Caching is easy, invalidation is the hard part. I'd start with a TTL I can defend from how often the data actually changes, and only build event-based invalidation for the things where staleness is genuinely unacceptable — pricing yes, catalog descriptions no."*

**What NOT to cache:** inventory counts and credit limits. If you cache "47 units available" and two retailers both see it, you oversell. Those reads go to the database, and that's a deliberate decision you should say out loud.

## 3.5 Denormalisation and read models (CQRS)

**What it is.** Normalised data (no duplication, joins to assemble) is great for writing and correctness. Denormalised data (duplicated, pre-joined) is great for reading. **CQRS** just means keeping both: a normalised write model and one or more denormalised read models built from it.

**Example.** The "My Orders" screen needs order, line items, product names, product images, distributor name, and delivery status. Normalised, that's a six-table join on every load. Instead, when an order changes you write a flat `order_summary` row — or a JSON document — with everything the screen needs. The screen becomes one primary-key lookup.

**How the read model gets updated:** either synchronously in the same transaction (simple, consistent, couples write latency to it), or asynchronously from events (fast writes, eventually consistent, needs to handle out-of-order and replay).

| Pros                                               | Cons                                       |
| -------------------------------------------------- | ------------------------------------------ |
| Read path becomes trivially fast and cheap         | Data is duplicated, so it can drift        |
| Read and write models can scale separately         | Eventual consistency — the read model lags |
| Read model can be rebuilt from the source of truth | More moving parts and more code            |
| Each screen can have a model shaped exactly for it | You need a way to detect and repair drift  |

**When to use:** read-heavy screens with complex assembly — order lists, catalog browsing, the feed, dashboards. **When not to:** anything where you need the number to be exactly right right now, like stock at checkout.

**The interview line:** *"I'd keep the normalised model in Postgres as the source of truth and build a denormalised read model for the heavy screens, updated from events. The cost is that the read model is a few hundred milliseconds stale, which is fine for an order list and not fine for stock at checkout — so stock at checkout reads the source of truth."*

That sentence hits technical depth and judgement at once, because it names where the pattern *doesn't* apply.

## 3.6 Partitioning and sharding

**Two different things that get confused.**

**Partitioning** splits one table into pieces inside one database. Postgres does this natively. `orders` becomes `orders_2026_01`, `orders_2026_02`, and so on. Queries that filter by date only touch the relevant pieces, and dropping old data becomes instant instead of a massive delete.

**Sharding** splits data across *separate databases*. Retailers A–M on database 1, N–Z on database 2.

**Example of when partitioning pays.** Your `orders` table is 300 million rows and 95% of queries are for the last 30 days. Partition by month: queries scan one small partition instead of the whole table, and archiving last year is a one-second `DETACH`.

**Sharding is a one-way door and you should say so.** Once sharded you lose cross-shard joins, cross-shard transactions, and simple `COUNT(*)`. Every query needs the shard key. Rebalancing when a shard gets hot is a major project.

|                  | Pros                                                                                                     | Cons                                                                                                                                 |
| ---------------- | -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| **Partitioning** | Smaller indexes, faster scans, instant archival, stays one database so joins and transactions still work | Needs a sensible partition key. Queries without it hit every partition. Some operational overhead.                                   |
| **Sharding**     | No ceiling on write throughput or storage. Failure is isolated to one shard.                             | Lose cross-shard joins and transactions. Every query needs the key. Rebalancing is brutal. Hot shards are a real and common problem. |

**Choosing a shard key.** It should be something the vast majority of queries filter on. In B2B commerce that's `retailer_id` or `tenant_id`. If you shard orders by `order_id`, then "show me this retailer's orders" has to query every shard — you've made the common case the expensive one.

**The hot shard problem.** If one distributor does 30% of volume and you shard by distributor, one shard melts while the others idle. Fix by salting the key or giving that tenant its own shard.

**The interview line, and it's a strong one:** *"At around 80,000 orders a day, sharding would be premature — one Postgres primary handles that comfortably for years. I'd partition the orders table by month for query performance and cheap archival, and keep sharding in my back pocket. The trigger to actually shard would be the write rate approaching what one primary can take, or the dataset exceeding what fits on one machine's disk. I'd want to see that number before paying the sharding tax, because it's a one-way door."*

## 3.7 Connection pooling

**What it is.** Postgres spawns a whole OS process per connection, so connections are genuinely expensive. A few hundred idle connections degrade the server.

**Example of the failure.** You run 20 containers, each with a pool of 20 connections. That's 400 connections to a database happy with 100. Everything slows down, and under load the pool exhausts and *healthy* endpoints start timing out because they can't get a connection. This is one of the most common real production incidents and it looks like "the whole site is down" when actually one slow query is holding connections.

**The fix.** **PgBouncer in transaction-pooling mode** sits between the app and Postgres and multiplexes many client connections onto few server connections, releasing them at transaction end.

| Pros | Cons |
|---|---|
| Lets hundreds of app instances share a small number of real connections | Session-level features break — some prepared statements, advisory locks held across statements, `SET` state |
| Removes connection setup cost | Another component to run and monitor |
| Protects the database from connection floods | Can mask the real problem (a slow query) |

**The interview line:** *"With many app containers I'd put PgBouncer in front in transaction mode, because Postgres is process-per-connection and app-side pools multiply by instance count. The caveat is that session-level state breaks under transaction pooling, so no advisory locks held across statements."*

## 3.8 CDN and object storage

**What it is.** A CDN caches static content at servers physically close to users. Object storage (S3) holds files cheaply and durably.

**Example.** Product images for 50,000 SKUs. Never serve these from your application. Store in S3, serve through a CDN. A retailer in a small town gets the image from a nearby edge node instead of your Mumbai server, and your backend never sees the request at all.

**Specifically relevant to this user base:** generate multiple image sizes on upload and serve the small one to low-end phones on 3G. A 2 MB product photo on a metered connection is a real cost to a retailer, and serving a 40 KB thumbnail instead is a product decision as much as a technical one. **Say that in the interview** — it's exactly the product-sense axis.

**Also:** uploads should go **directly from the phone to S3 using a presigned URL**, not through your API. Otherwise every photo upload occupies an application server for the duration of a slow mobile upload.

| Pros | Cons |
|---|---|
| Massive offload — static assets never touch your servers | Invalidation is slow; use versioned URLs instead |
| Much lower latency for distant users | Costs money per GB served |
| Absorbs traffic spikes for free | Only helps static or cacheable content |

**The interview line:** *"Images go to S3 behind a CDN, uploaded directly from the client with presigned URLs so they never touch my API, and I'd generate a thumbnail on upload because the user base is bandwidth-constrained."*

---

# Part 4 — Doing work later: queues, events, and async

## 4.1 The core idea

**What it is.** Instead of doing everything before responding to the user, do the essential part now and the rest in the background.

**Example.** Retailer places an order. What must happen before you respond? Validate, check credit, reserve stock, create the order. That's it — maybe 50ms. What can happen after? Send the SMS, email the distributor, update analytics, recompute recommendations, notify the brand, update the loyalty points. If you do all of it synchronously, the response takes 2 seconds and **any one of those failing fails the order**, which is absurd — the order is real, the SMS is not.

**The rule:** *if the user's intent is satisfied without it, it goes async.*

| Pros | Cons |
|---|---|
| Fast responses — users only wait for what matters | Eventual consistency; things happen "soon," not now |
| Failures in side effects don't fail the main action | Much harder to debug — no single stack trace |
| Absorbs bursts; the queue is a shock absorber | Needs idempotent consumers, because delivery is at-least-once |
| Components scale independently | More infrastructure, more ways to be wrong |

**The interview line:** *"Order creation is synchronous because the retailer needs a yes or no. Everything downstream — notifications, distributor push, analytics, recommendations — is an event, because none of those should be able to fail an order."*

## 4.2 Queue or event log?

**A queue** (SQS, RabbitMQ, a Postgres table) is for *work*: one consumer does the job, then the message is gone. Good for "send this SMS."

**An event log** (Kafka) is for *facts*: many independent consumers read the same stream, and the log can be replayed. Good for "OrderPlaced happened," where notifications, analytics, and the distributor integration each care independently.

|                       | Pros                                                                                                                                            | Cons                                                                                                   |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **Queue**             | Simple. Per-message retries, delays, dead-letter queues built in. Easy to run.                                                                  | One logical consumer. No replay.                                                                       |
| **Event log (Kafka)** | Many consumer groups read the same stream. Replayable — add a new consumer and reprocess history. High throughput. Ordering within a partition. | Operationally heavy. No per-message ack. Ordering only within a partition. Overkill for small volumes. |

**The honest judgement call to voice:** *"At one order per second, Kafka is hard to justify on throughput grounds alone — a Postgres-backed queue with `SELECT ... FOR UPDATE SKIP LOCKED` would do the job with zero new infrastructure. I'd bring in Kafka when I have several independent teams consuming the same events, or when I want replay. Those are the real reasons, not throughput."*

That answer is gold for the judgement axis, because the expected answer is "use Kafka" and you're declining with a reason and a named trigger.

## 4.3 The transactional outbox — the pattern to know by name

**The problem.** You need to save the order to Postgres *and* publish an `OrderPlaced` event. These are two different systems, so there's no shared transaction. If you commit the order and then crash before publishing, the order exists but nobody downstream knows — no SMS, no distributor notification. If you publish first and the commit fails, you've announced an order that doesn't exist.

**The fix.** In **one local transaction**, write the order row *and* a row into an `outbox` table. That's atomic — both or neither. A separate relay process reads unsent outbox rows, publishes them, and marks them sent.

**Why it works.** The only thing that can go wrong now is the relay crashing *after* publishing but *before* marking the row sent, which means the event gets published twice. And duplicate events are a solved problem — **idempotent consumers**. You've turned an unsolvable problem (atomicity across two systems) into a solved one (deduplication).

| Pros | Cons |
|---|---|
| No lost events, ever | Events are published with a small delay |
| No new infrastructure needed if you poll the table | Needs a relay process to run and be monitored |
| Uses a transaction you already have | Consumers must be idempotent |
| The outbox table doubles as an audit trail | Table needs cleanup or it grows forever |

**The interview line:** *"I'd use a transactional outbox. The order row and the event row go in the same transaction, and a relay publishes from the outbox with `FOR UPDATE SKIP LOCKED` so multiple relay instances don't collide. It publishes at-least-once, so consumers are idempotent. That's the standard way to make the database and the event stream agree without a distributed transaction."*

**This is your Kazam work in general form — lead with it when events come up.**

## 4.4 Idempotency — your strongest card, generalised

**What it is.** An operation is idempotent if doing it five times has the same effect as doing it once.

**Why it's unavoidable.** A timeout tells you nothing. When a mobile client's request times out, you don't know whether the server never got it, got it and is still working, or finished and the response got lost on the way back. So the client retries. So duplicates happen. So **operations must be idempotent**. There is no way around this chain.

**Especially here.** Your users are on patchy networks and will tap "Place Order" repeatedly on a frozen screen. **Duplicate submission is the normal case, not the exception.** Say that sentence in the interview — it's product sense and technical depth at once.

**How to build it.** The client generates an idempotency key per logical order attempt — one key per intent, the same key on every retry. The server has a table with a **unique constraint** on that key. On each request:

1. Try to insert the idempotency row: `INSERT ... ON CONFLICT DO NOTHING`.
2. If you inserted it, you own this operation — do the work, store the response.
3. If you inserted zero rows, someone else owns it — return their stored response, or a 409 if it's still in flight.

**The critical detail:** the **database's unique constraint** decides the winner, not your application code. "Check if it exists, then insert" is a race — two pods can both pass the check in the same millisecond. Interviewers listen for this exact mistake.

**And:** a duplicate returns the **stored original response**, not a re-run. Idempotent doesn't just mean "doesn't do damage twice," it means "gives the same answer."

| Pros | Cons |
|---|---|
| Makes retries safe, which makes everything else possible | Extra table and an extra write per request |
| Protects against double-tap, network retries, duplicate webhooks | Keys need expiry or the table grows forever |
| Required for at-least-once messaging to work at all | Clients have to generate and reuse keys correctly |

**The phrase that signals seniority:** *"Exactly-once delivery across a network is impossible. What you build is at-least-once delivery plus idempotent consumers, which gives you effectively-once processing."*

## 4.5 Sagas — multi-step operations that can fail halfway

**The problem.** Placing an order touches inventory, payment and fulfilment. If these are separate services with separate databases, there's no transaction spanning them. So what happens when payment fails after you've already reserved stock?

**The answer: a saga.** A sequence of local steps, each with a **compensating action** that undoes it.

> Reserve inventory → authorise payment → confirm order → notify distributor
>
> If payment fails: release the reservation.
> If the distributor rejects: void the authorisation and release the reservation.

**The key insight to say out loud: compensation is semantic, not literal.** You can't un-send an SMS, so you send a correction. You can't un-charge a card, so you refund. The system visibly passes through intermediate states and the business has to accept that.

**Two refinements worth naming.** A **semantic lock** is marking a record as in-progress — an order in `pending` state — so other operations know it isn't final. A **pivot transaction** is the point of no return; order your steps so the reversible ones come first and the irreversible one comes late, and failures get much cheaper.

| Pros | Cons |
|---|---|
| Works across services with no distributed transaction | Intermediate states are visible to users |
| Each step is a simple local transaction | You have to write and test every compensation |
| Failure handling is explicit rather than hoped-for | Debugging a half-finished saga is genuinely hard |
| Scales — no locks held across the network | More code than a single transaction |

**The judgement line that scores:** *"At this scale I'd keep order, inventory and payment in one service and one database, so the whole thing is a single Postgres transaction and I don't need a saga at all. Sagas are what you reach for when you've split those services — and I'd want a real reason to split them first, because a transaction is simpler and more correct than any saga I can write."*

**That is one of the best answers available to you in this round.** The expected answer is to design a saga. Declining to need one, with a reason, is stronger.

---

# Part 5 — The subsystems of a B2B commerce platform

This is the meat. Each subsystem follows the same shape: what it is, the naive version, why it breaks, how you actually build it, pros and cons, and the trap the interviewer is waiting for.

**A note on B2B versus B2C, because it matters throughout.** Amazon sells one unit to one person at one price. A B2B platform sells cases to a shop, at a price that depends on who's buying, often on credit, from a distributor who may only be able to supply part of the order. Every subsystem below is harder than its B2C equivalent for those four reasons: **negotiated pricing, credit, partial fulfilment, and distributor geography.**

## 5.1 Catalog

**What it is.** The list of products — SKUs, names, images, pack sizes, brands, categories.

**The naive version.** One `products` table, queried directly for every screen.

**Why it breaks.** A product isn't one thing. Parle-G exists as a single packet, a 12-pack, and a case of 144. Different distributors carry different subsets. Some products are regional. The same physical product has different names in different distributors' systems. And the catalog screen is your highest-traffic endpoint by a wide margin.

**How to build it.**

Separate three concepts that beginners merge into one:

- **Product** — the abstract thing. "Parle-G biscuits."
- **Variant / SKU** — the sellable unit. "Parle-G 800g case of 12." This is what has a barcode.
- **Offer / listing** — a specific distributor selling a specific SKU in a specific region. This is what has stock and a price.

So one product has many SKUs, and one SKU has many offers. A retailer browsing sees SKUs filtered to those with a live offer from a distributor who serves their pincode.

Then: **normalised write model in Postgres, denormalised read model for browsing.** The read model is a flat document per SKU per region holding everything the screen needs, rebuilt asynchronously when the underlying data changes. Serve all browsing from that.

| Pros of the read model                                        | Cons                                 |
| ------------------------------------------------------------- | ------------------------------------ |
| Catalog screen becomes one lookup instead of a six-table join | Stale for seconds after a change     |
| Survives a database problem if cached                         | More code and a rebuild pipeline     |
| Can be shaped per screen and per client version               | Drift between models needs detecting |

**The trap:** they'll ask *"a brand updates the price of one SKU — how long until retailers see it, and what updates?"* Have the answer ready: an event fires, the read model for that SKU is rebuilt, caches keyed on that SKU are invalidated or versioned, and the propagation time is a number you should state — "about a minute end to end, and that's a deliberate choice because a minute of stale catalog data is harmless."

**The follow-up trap:** *"what if it's the price, and the retailer places an order at the old price?"* The answer: **price is re-resolved at order time against the source of truth, and the displayed price is an estimate.** If they differ beyond a tolerance, show the retailer the new price and ask them to confirm. Never silently charge a different price than the one displayed — that's a trust problem, not a technical one. Saying that is product sense.

## 5.2 Pricing — the subsystem that makes B2B hard

**What it is.** What price does *this* retailer pay for *this* SKU *right now*?

**Why it's hard.** In B2C the price is a property of the product. In B2B it depends on the retailer's tier or segment, their region, which distributor serves them, volume slabs (10 cases is cheaper per unit than 2), active promotions and brand schemes, their negotiated terms, and sometimes a time window.

**The naive version.** A `price` column on the product. Breaks immediately.

**The naive-but-worse version.** Precompute every retailer times every SKU. With 4 million retailers and 50,000 SKUs that's 200 **billion** rows. Say that number out loud in the interview — showing you checked an approach and rejected it on arithmetic is exactly the right instinct.

**How to build it.** Two layers:

1. **Price lists per segment.** Group retailers into segments — region times tier times distributor is usually enough, giving maybe a few thousand combinations. Precompute a price list per segment. Now it's thousands of lists, not billions of rows, and a lookup is one key.
2. **Resolve the rest at read time.** Volume slabs, active promotions and retailer-specific overrides get applied on top, from a small rule set, per request. That's cheap because it's a handful of rules, not a database scan.

Cache the segment price list in Redis with a short TTL. Resolve the per-request part live.

| Pros | Cons |
|---|---|
| Lookup is fast and the key space stays manageable | Segment definitions become a business dependency |
| New promotions don't need a full recompute | Price logic now lives in two places — list and rules |
| Easy to explain to the business | Retailer-specific negotiated prices are an awkward special case |

**The trap:** *"how do you make sure the price in the cart is the price they're charged?"* The answer: **freeze the price onto the order line when the order is created.** The order stores the price it was placed at, not a reference to a price that can change underneath it. Same for tax and discount. If you don't do this, re-reading an old order shows today's price and your accounting is wrong forever. This is one of the most common real bugs in commerce systems, and naming it unprompted is a strong signal.

## 5.3 Inventory — where correctness actually matters

**What it is.** How many units are available, and never promising what you don't have.

**The naive version, and the bug nearly everyone writes:**

```
stock = SELECT available FROM inventory WHERE sku_id = 1
if stock >= qty:
    UPDATE inventory SET available = available - qty WHERE sku_id = 1
```

**Why it breaks.** Two retailers order the last 5 cases at the same moment. Both read `available = 5`. Both pass the check. Both decrement. Stock is now negative and you've sold product that doesn't exist. This is a **race condition**, and it's the single most likely thing you'll be asked to spot in this round.

**The fix — let the database decide:**

```sql
UPDATE inventory
SET available = available - :qty
WHERE sku_id = :id AND available >= :qty
```

This affects either **one row** or **zero rows**. Zero means insufficient stock. There is no window between the check and the write, because they are the same statement. The database holds a row lock for its duration, so the second request waits and then correctly fails.

**The other correct option** is `SELECT ... FOR UPDATE`, which locks the row so the two requests queue up. Slightly more flexible when you need to do other work between reading and writing, slightly more expensive.

**Reserve versus decrement — the B2B refinement.** Don't decrement at "add to cart" or abandoned carts hold stock forever. Don't decrement only at delivery or you oversell constantly. The pattern:

- **Add to cart:** nothing happens to stock.
- **Place order:** create a **reservation** with an expiry — say 30 minutes, or until payment confirms.
- **Payment confirms:** convert the reservation into a committed decrement.
- **Reservation expires or payment fails:** a background job releases it.

So `available = on_hand - reserved`.

| Pros of reservations | Cons |
|---|---|
| No overselling and no permanently locked stock | More states to manage and a cleanup job to run |
| Honest availability shown to other buyers | The expiry window is a business decision you have to defend |
| Gives payment a window to complete | A crashed cleanup job leaves stock locked — needs monitoring |

**The trap: do NOT cache inventory counts.** If you cache "47 available" and serve it to a hundred users, you oversell. The number on a browse screen can be approximate and cached — "In stock" or "Low stock" is enough — but **the number checked at order placement must come from the source of truth inside the transaction.** Saying this distinction out loud (approximate for display, exact for commitment) is precisely the technical-depth signal they want.

**The hot SKU problem.** If one SKU is wildly popular, every order contends on that one row and everything serialises behind it. The standard fix is splitting the row into N buckets of stock updated independently, picking one at random — trading exactness at the margins for parallelism. At this scale you almost certainly don't need it, and *"I wouldn't build that yet, but here's the mechanism if one SKU ever became the bottleneck"* is the ideal answer.

## 5.4 Cart and order placement

**What it is.** The flow from "retailer has items selected" to "an order exists."

**Cart design.** A cart is low-value, high-churn data. It can live in Redis with a TTL, or in Postgres if you want it durable and analysable. **For this user base, persist it** — a retailer on a flaky connection who loses their cart because their phone dropped off 3G will not rebuild it. That's a product judgement, and framing it that way scores.

**The order placement transaction** is the heart of the system. What belongs inside it:

1. Insert the idempotency key row — the unique constraint wins the race.
2. Validate the cart and re-resolve prices from the source of truth.
3. Check the retailer's credit limit.
4. Reserve inventory with the conditional update.
5. Insert the order and line items, with prices frozen onto the lines.
6. Insert the outbox row for `OrderPlaced`.
7. Commit.

What stays **outside** it: calling the payment gateway, calling the distributor's API, sending the SMS, updating analytics. **Never make a network call to a third party inside a database transaction.** If their API hangs for 30 seconds you've held locks for 30 seconds and the whole system backs up behind you. That's a specific, concrete, senior thing to say.

**Partial fulfilment — the B2B reality.** The distributor often can't supply everything. So an order is not atomic from the business's point of view. Per line item the model needs ordered quantity, confirmed quantity, delivered quantity, and a reason for any gap. **Make partial fulfilment a first-class state, not an error.** A model that assumes every order is either fully fulfilled or cancelled gets rewritten within three months, and saying so shows you understand the domain rather than e-commerce in the abstract.

| Pros of one transaction                | Cons                                        |
| -------------------------------------- | ------------------------------------------- |
| Correctness guaranteed by the database | Everything involved must be in one database |
| Simple to reason about and test        | The transaction must stay short             |
| No saga and no compensation logic      | Stops working once services are split       |

**The trap:** *"two pods get the same request in the same millisecond."* The idempotency insert with a unique constraint — not an application-level check. Full treatment in §4.4.

**The second trap:** *"the retailer's phone loses connection right after they tap, and the app retries. What happens?"* Same idempotency key, so the second request finds the row already there and returns the stored response. One order. **This is your Kazam work — say so explicitly:** "this is exactly the problem I solved at Kazam, where the three parties were us, the payment gateway, and the charging network."

## 5.5 Payments and credit

**B2C payments** are: charge a card, get a yes or no. **B2B payments** are mostly credit — a retailer orders today and pays in 7, 14 or 30 days. That changes everything.

**A credit limit per retailer**, with an available-credit calculation that accounts for orders placed but not yet paid. The check at order time has the same shape as the inventory check: a conditional update, not a read-then-write, or two concurrent orders can both pass a limit they jointly exceed.

**A ledger.** This is the part people get wrong. A ledger is **append-only** and **double-entry**: every entry has a matching opposite entry, and debits equal credits. You **never edit a posted entry** — to reverse something, you post a compensating entry. The balance is derived from the entries, not stored as a mutable number you update in place.

Why so strict? A mutable balance column is a number you can't audit. When it's wrong — and it will be — you have no way to find out when or why. With an append-only ledger you replay history and find the exact entry that broke.

**Reconciliation.** Every day, compare your ledger against the payment provider's settlement file. Bucket the results: matched, missing on your side, missing on theirs, amount mismatch. Timing differences clear themselves on the next run. Real breaks go to a human with enough context to act.

**This is literally your resume. Lead with it.** *"I built exactly this at Kazam — automated ledger reconciliation against the provider's settlement file, which removed five to eight manual reconciliations a week."*

| Pros of an append-only ledger | Cons |
|---|---|
| Fully auditable — you can always explain a balance | More rows; balances need computing or caching |
| Corrections leave a trail instead of hiding | Developers have to resist the urge to just `UPDATE` |
| Reconciliation becomes mechanical | More design work upfront |

**Money storage:** integer paise or `NUMERIC`. **Never floating point.** 0.1 can't be represented exactly in binary floating point, and in a ledger those tiny errors pile up into reconciliation breaks that take days to find.

**The trap:** *"how do you know you never lost a transaction?"* The honest answer is **not** "my code was correct." It's **"I had an independent check"** — the reconciliation job compares against an external source, invariants are asserted continuously, and drift raises an alert. You know because something other than the happy path was checking. Your resume says "zero data loss," so expect this question.

## 5.6 Fulfilment, logistics and distributor integration

**What it is.** Getting the order from the distributor to the shop, and keeping everyone informed.

**The core difficulty: you don't control the distributor's systems.** Some have APIs. Some have a portal a human logs into. Some get a WhatsApp message. Your platform has to work across all of them.

**How to build it.** An **adapter per distributor** behind one internal interface. Your order service emits `OrderPlaced`; a fulfilment service picks it up and routes to the right adapter — API call, file drop, or a task in a human-operated queue. The rest of your system neither knows nor cares which.

Handling their unreliability:

- **Per-partner timeouts**, based on that partner's actual latency rather than a round number.
- **Retries with exponential backoff and jitter.** Jitter matters — without it your retries sync up and hammer them all at once.
- **A circuit breaker per distributor:** if one is failing, stop calling it for a cooldown and fail fast instead of piling up requests. When a dependency is down, retrying makes it worse.
- **Quarantine a misbehaving partner** rather than letting it degrade everything.
- **Reconciliation** against their system of record, because their state and yours will drift.
- **Out-of-order updates** handled with version numbers or source timestamps — a "delivered" webhook can arrive before "dispatched."

**You have done this exact thing.** The Beckn work was fan-out to HPCL/BPCL partner networks with no control over the other side's quality. Say so: *"this is structurally the same as the partner integration work I did at Kazam — unreliable third parties, async callbacks, partial results, and reconciliation to catch drift."*

| Pros of the adapter pattern | Cons |
|---|---|
| A new distributor is one new adapter, no core changes | Adapters proliferate and each needs maintenance |
| Core system stays clean | Testing needs mocks or sandboxes per partner |
| Per-partner failure isolation | Normalising wildly different data models is real work |

**The trap:** *"what if a distributor confirms an order and then can't deliver half of it?"* Partial fulfilment again. The order moves to a partially-fulfilled state, the retailer is notified, the undelivered lines are either cancelled with a credit note or backordered, and the ledger reflects only what was delivered.

## 5.7 Returns, refunds and credit notes

Candidates skip this, and it's where B2B gets genuinely messy.

A return can be damaged goods, a wrong item, expired stock, or unsold inventory going back. Each has different financial treatment. In a credit-based system the "refund" usually isn't money moving at all — it's a **credit note** reducing what the retailer owes.

The rules: **never mutate the original order.** Create a return or credit-note record that references it. Post a compensating ledger entry. Restore inventory only if the goods are actually resaleable. And handle the awkward case of a return against an order already settled with the distributor.

**The interview line:** *"Returns are append-only too. I don't edit the original order, I create a linked return document and post a compensating ledger entry, so history stays intact and auditable."*

## 5.8 The community feed

Kirana Club is explicitly community-led, so this will probably come up. It's also the one subsystem here with a genuinely different shape from the rest.

**The problem.** Retailers post, comment and form groups. When someone posts, who sees it and when?

**Fan-out on write** — when someone posts, immediately write that post ID into every follower's timeline. Reads become one lookup of a pre-built list.

**Fan-out on read** — store the post once. When a user opens the feed, query everyone they follow and merge.

|                      | Pros                                                     | Cons                                                                                                       |
| -------------------- | -------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Fan-out on write** | Reads are instant and cheap. Scales to huge read volume. | Writes are expensive. One post by someone with 500,000 followers means 500,000 writes. Storage duplicated. |
| **Fan-out on read**  | Writes are trivial. No duplication.                      | Reads are expensive and get slower the more people you follow.                                             |

**The standard production answer is hybrid:** fan out on write for normal accounts, and for the few accounts with enormous followings, skip the fan-out and merge their posts in at read time. Best of both, at the cost of two code paths.

**For this user base, two things matter more than the fan-out strategy.** **Cursor pagination** — never `OFFSET`, which gets slower the further you scroll and skips or duplicates items when new posts arrive mid-scroll. And **aggressive payload trimming** with small images, because bandwidth is a real cost to the user.

**The trap:** *"what's your ranking algorithm?"* Resist designing a machine learning system. Start with reverse-chronological plus simple signals — recency, engagement, same region, same product category. **Say it as a choice:** *"I'd start chronological because it's explainable and shippable this week, and only add ranking once I have engagement data showing people aren't finding what's relevant. Ranking with no data to train on is guessing."*

## 5.9 Notifications

**What it is.** SMS, push, WhatsApp, in-app. Boring, and a common source of production pain.

What matters:

- **Always async.** A notification must never be able to fail an order.
- **Idempotent** — a retried event must not send a second SMS. Key on event ID.
- **Rate-limited and batched per user**, or a bug sends someone 400 messages and you've burned both trust and money.
- **Templated and localised** — this user base needs vernacular languages, which means templates with placeholders, not string concatenation in code.
- **Preference-aware** — honour opt-outs and quiet hours.
- **Fallback chain** — push fails, try SMS. Cheapest channel first.

**The cost angle, which is product sense:** SMS costs real money per message at millions of users. Push is nearly free but needs the app installed. WhatsApp sits in between with template approval requirements. **Pointing out that channel choice is a unit-economics decision, not just a technical one, will stand out.**

## 5.10 Search

**What it is.** A retailer types "parle" or "biscuit" or a misspelling and gets useful results.

**Why Postgres full-text eventually isn't enough.** It's genuinely good — `tsvector` with a GIN index handles a lot. But you'll want typo tolerance, synonyms, faceting by category and brand, and relevance ranking you can tune. That's what Elasticsearch is for.

**The architecture:** Postgres stays the source of truth. Changes flow to Elasticsearch asynchronously, via the outbox or CDC. Search queries hit Elasticsearch and get back IDs; you either serve the denormalised document straight from the index or hydrate from Postgres.

| Pros of a search index | Cons |
|---|---|
| Typo tolerance, synonyms, relevance tuning, facets | A second system to run, monitor and scale |
| Takes search load off the primary database | Eventually consistent with the source of truth |
| Fast aggregations for filters | Needs a reindex strategy and drift detection |
| Can be rebuilt from Postgres if lost | Easy to start treating it as a source of truth |

**The judgement answer:** *"I'd start with Postgres full-text search and a GIN index, because it handles the common cases with zero new infrastructure. I'd move to Elasticsearch when I need typo tolerance and synonyms — and for a user base typing product names in several languages and transliterations, that's probably sooner rather than later. But I'd want to see the search-failure rate before paying for a cluster."*

**Specific to India, and worth saying:** people search in Hindi, in English, and in Hinglish transliteration — "चाय", "chai", "tea". That's a synonym and transliteration problem as much as a relevance problem, and it needs a curated synonym list, not just a cleverer algorithm.

## 5.11 Analytics and reporting

**The mistake:** running heavy analytical queries against your production database. One `GROUP BY` over a year of orders ties up resources and slows the order path, and an outage caused by someone's dashboard is a bad day.

**The fix:** separate them. The simple version is running reports off a read replica. The grown-up version is pushing data into a columnar store — ClickHouse, BigQuery, Redshift — where analytical queries belong.

**The judgement line:** *"At this volume a read replica for reporting is enough and costs almost nothing. I'd move to a proper warehouse when queries start taking minutes, or when the business wants to join order data with sources outside the platform."*

## 5.12 Multi-tenancy and onboarding distributors

**You've done this twice** — Node.js at Kazam for 20+ OEM tenants, Django at Alemeno for 12+ diagnostic centres. **The contrast between them is one of your best available answers.**

| Model | Pros | Cons |
|---|---|---|
| **Shared schema, `tenant_id` column** | Cheapest to run. One migration. Scales to many tenants. | One missing `WHERE tenant_id` is a data breach. One noisy tenant affects everyone. |
| **Schema per tenant** | Real separation, per-tenant customisation possible. | Every migration becomes N migrations. Postgres strains past a few hundred schemas. |
| **Database per tenant** | Strongest isolation, per-tenant backup and restore, often needed for compliance. | High operational cost per tenant. |

**The question they'll ask: how do you prevent cross-tenant leakage?** The weak answer is "we're careful." The strong answer is layered:

1. **Postgres Row-Level Security**, so the database enforces it even when application code forgets. This is the differentiator — most candidates never mention it.
2. A mandatory data-access layer that injects the tenant filter, making an unscoped query impossible to write.
3. Tenant resolved once per request from the signed token, never from a client-supplied header.
4. **Tests that explicitly assert tenant A cannot read tenant B's rows.** Test the attack, not just the happy path.

**The interview line:** *"I've built both — shared schema with a tenant column at Kazam, and schema-per-tenant with django-multitenants at Alemeno. For a platform onboarding hundreds of distributors I'd use shared schema with Row-Level Security, because schema-per-tenant turns every migration into N migrations and doesn't scale past a few hundred. RLS gives me database-enforced isolation without the migration tax."*

---

# Part 6 — Cross-cutting concerns

These apply to every subsystem. They're also where interviewers go when they want to check you've run something in production rather than just designed it.

## 6.1 Rate limiting

**Why you need it.** One buggy client, one scraper, or one retailer whose app is stuck in a retry loop can consume capacity meant for everyone.

**Where it goes.** At the edge — API gateway or Nginx — not in each service. And in Redis, not in process memory, or your limit multiplies by the number of instances (see §2.6).

**The algorithms:**

| Approach | Pros | Cons |
|---|---|---|
| **Fixed window** | Simplest to implement and explain | Allows a 2x burst right at the window boundary |
| **Sliding log** | Exact | Stores every request timestamp — memory-heavy |
| **Sliding window counter** | Good accuracy, cheap | Slightly approximate |
| **Token bucket** | Allows controlled bursts, which matches real usage | Two parameters to tune |

**The product-sense point:** rate limits for this user base should be generous and should return `429` with a `Retry-After` header, because the clients are retry-heavy *by necessity*, not by abuse. Punishing a retailer on a bad connection for retrying is punishing them for their network. **That sentence is exactly the kind of thing that gets remembered.**

## 6.2 The hot key / celebrity problem

**What it is.** Traffic is never evenly spread. One SKU goes viral, one distributor does 30% of volume, one brand runs a campaign. Whatever you partitioned or sharded by, one of them will be hot.

**Where it shows up:** a hot cache key (all reads hit one Redis node), a hot database row (all writes contend on one row), a hot partition (one shard melts while others idle).

**Fixes:** local in-process caching in front of the shared cache for genuinely hot reads; splitting the hot row into buckets for writes; salting the key; or giving the hot tenant its own dedicated resources.

**The interview line:** *"I'd design for the common case and monitor for skew rather than pre-solving it, because which key goes hot is usually not predictable. The thing I'd put in place from day one is per-key metrics so I can see it happening."*

## 6.3 Graceful degradation

**What it is.** When part of the system is down, serve something useful instead of an error.

**Examples.** Recommendation service down? Show the catalog unranked. Search cluster down? Fall back to a simple database query with no typo tolerance. Credit service slow? Let a retailer with plenty of headroom through on a cached limit, but block anyone near their limit.

That last one is a good example to give, because it shows you can **degrade differently depending on risk**, rather than treating the whole system as one on/off switch.

| Pros | Cons |
|---|---|
| Partial outages don't become total outages | More code paths, and they're rarely tested |
| Users often don't notice | Degraded mode can hide a real outage from you |
| Buys time to fix things properly | Needs an explicit decision per feature |

**The interview line:** *"I'd decide per feature what degradation looks like. Browsing should survive almost any failure. Order placement should fail loudly rather than quietly accept an order we can't fulfil — a false 'yes' is worse than an honest error."*

## 6.4 Observability

You can't fix what you can't see. The three things:

- **Structured logs with a correlation ID** carried through every hop, so one request is one query instead of a manual join across services.
- **Distributed tracing**, so you know *which* of twelve hops ate the latency instead of guessing.
- **Metrics** — RED per endpoint (Rate, Errors, Duration) and USE per resource (Utilisation, Saturation, Errors).

Two things that mark experience: **alert on symptoms users feel, not on CPU** — error rate and latency, not resource graphs. And **measure percentiles, never averages** — the mean hides everything, and p99 is where your worst-served customers live.

**The business-aware version, which is better:** alert on business metrics too. A sudden drop in orders per minute catches problems no technical metric will — a broken deploy that returns 200 with an empty catalog looks perfectly healthy on every infrastructure dashboard. **This is a great thing to volunteer.**

## 6.5 Deploys, migrations and zero downtime

**The thing most candidates miss.** During a rolling deploy, old and new code run at the same time against one database. So any migration must be safe for both.

**The expand/contract pattern** (also called parallel change):

1. **Expand** — add the new column as nullable. Old code ignores it, new code can use it.
2. **Backfill** — populate it in batches, not one giant `UPDATE` that locks the table.
3. **Migrate** — deploy code that writes both and reads the new one.
4. **Contract** — once nothing reads the old column, drop it.

Never: rename a column in one step, add `NOT NULL` with a default to a huge table in one step, or build an index without `CONCURRENTLY` on a live table.

**The interview line:** *"Migrations use expand/contract, because during a rolling deploy both versions of the code are live against the same schema. A rename is three deploys, not one."*

## 6.6 Security basics worth naming

- **Authentication:** short-lived JWT with identity, tenant and scopes, validated at the gateway. Know the trade-off — stateless and fast, but **you can't revoke one before it expires** without adding state back, which is why access tokens are short-lived with a revocable refresh token behind them.
- **Authorisation at the data layer, not just the endpoint.** Middleware guards the route; only a data-layer check guards the rows.
- **Never trust the client.** Price, tenant ID, user ID and totals all get resolved server-side. A client-supplied price is the classic commerce vulnerability.
- **Presigned URLs** for uploads so files never pass through your API.
- **Secrets in a secret manager**, not environment variables committed anywhere.
- **PII:** phone numbers are PII. Encrypt at rest, mask in logs, and think about who can query them.

---

# Part 7 — The user base is the architecture

This is the product-sense axis, and it's the easiest place to stand out, because most candidates design for a user who has an iPhone and fibre.

## 7.1 Who actually uses this

Kirana store owners in Tier II–IV towns and rural India. In practice that means: low-end Android phones with limited RAM, patchy 3G or 4G, metered data plans where every megabyte has a cost, often not English as a first language, frequently one person running the shop and the phone at the same time, and limited patience for anything confusing.

## 7.2 What that means for the backend — say these unprompted

**Payload size is a feature.** Trim every response. Don't send fields the screen doesn't use. Compress. Paginate small. A 2 MB catalog response costs the retailer actual money, and on a slow connection it may simply never finish. **Design the API around a payload budget.**

**Clients will retry constantly, so the server must be idempotent.** A frozen screen gets tapped four times. Duplicate submissions are **the normal case, not an edge case**. This is your strongest card — play it here.

**Design for offline and intermittent connectivity.** Let the app cache the catalog and work degraded. Queue actions locally and sync when the connection returns. Which means the server has to accept a submission with an old timestamp and an idempotency key, and handle them arriving out of order.

**Prefer polling or SSE over WebSockets.** A WebSocket on a flaky mobile network reconnects constantly, burning battery and data and churning server connections. For order status updates, polling with a sensible interval is often genuinely better engineering.

**Serve small images.** Generate thumbnails on upload. Never send a full-resolution product photo to a phone showing it at 100 pixels wide.

**Localisation is a data problem, not a string problem.** Product names, units and categories need translations in the data model, not just UI strings. And search needs to work across scripts and transliterations.

**Latency from the user's phone matters more than your server p99.** Your service can respond in 50ms and the user still waits 3 seconds because of mobile network round trips. **Fewer round trips beats faster round trips** — which is an argument for a backend-for-frontend that aggregates several calls into one.

## 7.3 The sentence that lands

*"The thing that changes my design most here isn't the scale, it's the connection quality. A retailer on 3G tapping Place Order four times on a frozen screen has to produce one order, and the catalog screen has to fit in a payload they can actually afford to download. So idempotency and payload budget are design constraints from day one, not optimisations later."*

Say something like that early in the round. It hits product sense, business context and technical depth in one move, and it's a view most candidates won't have.

---

# Part 8 — Business problems and product sense

They told you "business problems" and "product and business sense" are scored. This part is how you handle a question like *"retailers order once and never come back — how would you fix that?"*

## 8.1 Start with the metric, not the system

The reflex to build is wrong. The first move is always:

> "Before I design anything — what's the metric we're moving, what is it now, and what would good look like? And do we know *why* they're not coming back, or are we guessing?"

That's not stalling. It's the most senior thing you can say, because **the most common engineering failure is building the right system for the wrong problem.**

## 8.2 The metrics that actually matter in B2B commerce

Know these. They'll come up, and using them correctly signals that you've thought about commerce as a business.

| Metric | What it means | Why it matters here |
|---|---|---|
| **GMV** | Gross merchandise value — total value of goods sold | The headline number, but it hides margin |
| **Take rate** | Your cut of GMV | GMV without take rate can be unprofitable growth |
| **AOV** | Average order value | In B2B, driving AOV up is often cheaper than acquiring users |
| **Order frequency** | Orders per retailer per month | The real engine of B2B — the same shop reordering |
| **Repeat rate / retention cohorts** | Share who order again after a first order | The single most important health metric for this business |
| **Fill rate** | Share of ordered units actually delivered | **The B2B killer.** A retailer who gets 60% of what they ordered stops trusting you |
| **Time to delivery** | Order to doorstep | Shops run on thin inventory; late means lost sales for them |
| **CAC and payback** | Cost to acquire, time to earn it back | Decides whether growth is worth it |
| **Credit default rate** | Share of credit not repaid | If you extend credit, this can kill the company |

**The one to lead with is fill rate.** In B2B grocery, trust is the product. A retailer orders 20 items and gets 12 — they go back to their old distributor and don't come back. **It's a supply problem that looks like a retention problem**, and saying that shows you can see past the obvious.

## 8.3 How to answer "retailers order once and never return"

Don't jump to features. Work it like this, out loud:

**1. Frame it as a funnel.** Where exactly do they drop? Registered but never ordered? Ordered once and never again? Ordering but declining in value? These are three completely different problems with three different fixes, and **naming that distinction is most of the score.**

**2. Form hypotheses and say how you'd check each.**

| Hypothesis | How you'd check it |
|---|---|
| The price wasn't actually better than their current distributor | Compare order prices against local market rates; survey churned users |
| Fill rate was bad — they didn't get what they ordered | Query fill rate for first orders of churned vs retained retailers |
| Delivery was late or unreliable | Compare promised vs actual delivery time by cohort |
| The catalog didn't have what they needed | Look at search queries that returned nothing |
| The app was too hard on their phone | Drop-off by screen; app performance by device tier |
| They forgot — no reorder prompt | Check whether any reminder exists at all |

**3. Say which you'd check first and why.** "I'd start with fill rate on first orders, because it's cheap to query, it's the most common cause in this business, and if it's bad no feature will fix it."

**4. Only then propose a system.** And start with the smallest thing. A reorder button with their last order pre-filled. A reminder based on their usual cycle. A "notify me when back in stock" so a stockout becomes a captured intent rather than a lost one.

**5. Say how you'd measure it.** "I'd ship it to 10% and compare 30-day repeat rate against a holdout."

**That five-step shape — funnel, hypotheses, cheapest check first, smallest intervention, measure — works for any business problem they throw at you.** Learn the shape, not the specific answer.

## 8.4 Other business prompts to have a shape for

**"How would you increase average order value?"** Reorder suggestions from their own history (cheapest and most effective), volume slab nudges ("2 more cases and the unit price drops"), bundles, and credit limit increases for reliable payers. Note the trade-off out loud: pushing AOV up with credit increases exposure to default, so it isn't free.

**"A brand wants to run a promotion. What do you build?"** Scope it: which SKUs, which regions, which retailer segments, what period, what budget cap. The hard parts are **stopping the promotion once the budget is exhausted** (a counter with a race condition — same pattern as inventory, which you should name), attribution for billing the brand, and making sure a promotion can't make the price negative or stack with another promotion in an unintended way.

**"How would you decide whether to build our own logistics?"** Don't answer yes or no. Answer with what you'd need to know: current third-party cost per delivery, their fill and on-time rate, order density per area (density is everything in logistics economics), and whether delivery is a differentiator or a cost centre for this business. Then: pilot in one dense cluster, measure, decide. **Refusing to answer a strategic question without data is correct, as long as you say exactly what data.**

**"Should we extend more credit?"** This is a risk question. More credit means more orders and more exposure. You'd want default rate by segment, repayment history as a scoring input, and limits that grow with proven behaviour rather than being set once. And you'd want to be able to turn it off per segment quickly.

---

# Part 9 — Problem decomposition

They score this separately, which means they'll give you something deliberately big and vague.

## 9.1 The method

**Step 1 — Restate it in one sentence.** "So we want a retailer to be able to order from multiple distributors in one basket and get one delivery. Is that right?" Confirm before you build.

**Step 2 — Split into sub-problems and name them.** Out loud, as a list. For the multi-distributor basket example:

1. Figuring out which distributors can serve this retailer and this SKU
2. Splitting one basket into per-distributor orders
3. Pricing when the same SKU has different prices from different distributors
4. Coordinating fulfilment so the retailer sees one delivery
5. Payment and settlement split across distributors
6. What happens when one distributor's part fails

**Step 3 — Rank them.** Which are easy and well-understood? Which are genuinely hard? Which are risky because you don't know enough?

> "One, two and three are mechanical — I know how to build those. Four is a coordination problem and it's where the design actually lives. Six is the one that will cause production pain. I'd spend our time on four and six."

**Step 4 — Go deep on the hard one.** Don't spread evenly. **Depth on the hard part beats surface coverage of everything**, and choosing correctly is itself the thing being scored.

**Step 5 — Say what you're deferring.** "I'm not going to design the settlement split now — it's real work but it's well-understood and it doesn't change the rest of the architecture."

## 9.2 The move that scores highest

**Separating the essential complexity from the accidental complexity.** In the example above, coordinating a split order across distributors is essential — the business genuinely requires it and no clever code makes it disappear. Pricing lookups are accidental — they're only hard because of how the data is laid out, and a better model makes them easy.

Saying *"this part is genuinely hard and we have to deal with it, this part is only hard because of a choice we made and we can fix the choice"* is a senior distinction most people never articulate.

---

# Part 10 — Prioritisation and tech judgement

The axis most candidates fail, because the instinct in an interview is to demonstrate everything you know.

## 10.1 The core skill is saying no, with a number

Bad: "We should add Kafka, a search cluster, and shard the database."

Good: *"None of those yet. At 80,000 orders a day one Postgres primary is fine, and adding infrastructure adds failure modes and on-call burden with no user-visible benefit. I'd add a read replica now because it's cheap and the read load is real. I'd revisit sharding when the write rate gets near what a single primary can take, or when the dataset outgrows one machine's disk. Those are the numbers I'd watch."*

**Every "no" needs a trigger attached.** "Not yet" without a threshold sounds like avoidance. "Not until X" sounds like judgement.

## 10.2 Build versus buy

Default to buying for anything that isn't your core differentiator. Payments, SMS, maps, auth, search infrastructure, monitoring — buy. Your pricing engine, your order lifecycle, your distributor integration layer — build, because they *are* the product.

| Buy | Build |
|---|---|
| Faster to ship, someone else is on call | Costs money forever and scales with usage |
| Usually more reliable than v1 of yours | You're limited by their roadmap and their outages |
| Frees your team for the differentiator | Data leaves your system — a real concern for PII |

**The interview line:** *"I'd buy anything that isn't the thing we're actually better at. The pricing engine and the order lifecycle are the product, so those we build. Payments and SMS are solved problems where my version would be worse."*

## 10.3 Technical debt — have a real position

Not all debt is bad. Debt taken knowingly, to learn something faster, with a note about when to pay it, is good engineering. Debt taken accidentally, because nobody thought about it, is the problem.

**The rule worth stating:** *"I'm relaxed about debt in things that are easy to change later and strict about debt in things that aren't. A messy internal service I'll clean up. A sloppy data model or a published API contract I won't ship, because those are the expensive ones to undo."*

That's the **one-way door versus two-way door** idea and it's the most useful framework you can bring to this axis. One-way doors: data models, API contracts other people have integrated with, anything a client caches, anything involving money. Two-way doors: internal service boundaries, caching strategy, library choices, queue technology.

## 10.4 "What would you do in your first 90 days?"

A likely closing question and an easy one to answer badly by promising rewrites.

The shape: **learn, then fix something small and real, then take on something structural.**

> "First couple of weeks: ship something small end to end so I learn the deploy pipeline, the review culture and where the bodies are buried. Alongside that, read the order and payment path closely, because that's where my experience is and where bugs are most expensive.
>
> Then I'd want to find the thing that pages people most often and fix that class of problem — not the instance, the class. That earns trust and it's genuinely useful.
>
> After that I'd want to own a surface end to end. But I'd want to be told what's most valuable rather than deciding alone, because I won't have the business context yet."

That last sentence matters. It shows you know what you don't know, which is the thing a founder actually worries about with a new hire.

## 10.5 When they ask you to defend a simple design

They may push: *"that seems too simple — what if we 10x?"* Don't panic and add infrastructure. Answer:

> "10x of 80,000 orders a day is 800,000, which is about 10 writes a second average. One Postgres primary still handles that. At 100x I'd be partitioning the orders table and moving reads to replicas, which I'd do anyway. The thing that actually breaks first isn't the database, it's [whatever you identified — probably the catalog read path or the feed fan-out], and that's the piece I'd design to scale from the start."

**Knowing which component breaks first is the real answer to a scaling question.** Everything scales eventually; the question is what breaks first and whether you've designed *that* part with room.

---

# Part 11 — Your resume in a round 2 context

Round 1's Appendix A covers defending your resume claim by claim. Round 2 asks something different: **can you generalise from what you built to what they need?**

For each line, know the bridge sentence.

| Your line                                          | The bridge to Kirana Club                                                                                                                                                                                       |
| -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Idempotent order/payment lifecycle, 20K daily txns | "Same problem exactly — retailers on bad networks double-tapping Place Order. The mechanism transfers directly: client-supplied key, unique constraint in the database, stored response returned on duplicate." |
| Ledger reconciliation, removed 5–8 manual/week     | "A B2B credit platform needs this more than we did, because the money sits outstanding for 30 days and the surface for drift is bigger."                                                                        |
| Beckn — fan-out to HPCL/BPCL partner networks      | "Distributor integration is the same shape: unreliable third parties you don't control, async callbacks, partial results, out-of-order updates, reconciliation to catch drift."                                 |
| Multi-tenant SaaS, 20+ OEM tenants, RBAC           | "Onboarding distributors and brands is multi-tenancy. I've done shared-schema and schema-per-tenant and can argue the trade-off from both sides."                                                               |
| Redis caching, 65% latency cut                     | "The catalog read path is the equivalent here — and the lesson I took was that invalidation, not caching, is the hard part."                                                                                    |
| LLM tool interfaces, 15+ agent workflows           | "The JD mentions evaluating AI output twice. I've built *for* models, not just with them — tool schemas, validation at the boundary, guardrails before an agent touches a financial API."                       |
| Pujo Atlas — 871K searches, burst traffic          | "Predictable spiky load. Festival traffic and a brand flash sale are the same shape: cache hard, read replicas, don't over-provision the write path."                                                           |

**The move:** when they describe a problem, say *"I've solved the structurally similar problem — here's what transfers and here's what's different."* The second half matters. Claiming it's identical when it isn't gets caught immediately.

**And be honest about the gaps.** You haven't run Kafka or Elasticsearch in production. If it comes up: *"I know the model but I haven't operated a cluster"* — then demonstrate the model anyway. Round 1's Appendix A §A.1 has the full list of unbacked skills-line claims and the honest downgrade sentence for each. Re-read it.

---

# Part 12 — Three worked examples

Do these out loud, with a timer, before the interview. Reading them is worth about a tenth of saying them.

## 12.1 "Design order placement for Kirana Club"

**Minute 0–3: Clarify.**

> "Before I design — how many retailers are actively ordering, and roughly how many orders a day? Is one order from one distributor or can it span several? Is payment upfront or on credit? And is this greenfield or am I extending something?"

Assume they say: ~80K orders/day, one distributor per order for now, mostly credit, greenfield.

**Minute 3–5: Math, out loud.**

> "80,000 a day is about one write per second average. Even at a 10x peak that's 10 a second — that's a small write rate, one Postgres primary handles it with enormous headroom. Reads will be much bigger: if 100,000 retailers browse and each loads 50 screens, that's 5 million reads a day, roughly 60 a second average and maybe 500 at peak. So this is read-heavy, maybe 60:1. Storage is under a gigabyte a day, so a few hundred GB a year — one machine for years.
>
> That tells me the write path isn't a scaling problem, it's a correctness problem. I'll keep it simple and strictly correct, and spend the scaling effort on the read path."

**Minute 5–9: Entities and API.**

> "Entities: Retailer, Distributor, SKU, Offer, Cart, Order, OrderLine, Reservation, Payment, LedgerEntry.
>
> API: `POST /orders` with an idempotency key, `GET /orders`, `GET /orders/{id}`, `POST /orders/{id}/cancel`. Catalog and cart are separate."

**Minute 9–16: Data model — slow down here.**

> "`orders`: id, retailer_id, distributor_id, status, total_amount in paise, placed_at, idempotency_key with a unique constraint.
>
> `order_lines`: order_id, sku_id, quantity_ordered, quantity_confirmed, quantity_delivered, unit_price_at_order, line_total. **Prices are frozen onto the line** — the order stores what was charged, not a pointer to a price that can change.
>
> **Quantity has three columns on purpose.** Partial fulfilment is normal in B2B, so it's a first-class state, not an error.
>
> `inventory`: sku_id, distributor_id, on_hand, reserved. Available is on_hand minus reserved.
>
> `reservations`: order_id, sku_id, quantity, expires_at.
>
> `ledger_entries`: append-only, double-entry, never updated.
>
> `outbox`: event rows written in the same transaction as the order.
>
> Indexes that matter: `(retailer_id, created_at DESC)` on orders for the order list, unique on idempotency_key, and `(sku_id, distributor_id)` on inventory."

**Minute 16–21: Happy path.**

> "Retailer taps Place Order. Client sends `POST /orders` with an idempotency key it generated for this attempt.
>
> One transaction: insert the idempotency row with `ON CONFLICT DO NOTHING` — if zero rows, someone else owns this request, return their stored response. Re-resolve prices from the source of truth. Check credit with a conditional update. Reserve inventory with `UPDATE ... WHERE available >= qty`, which affects one row or zero. Insert order and lines with frozen prices. Insert the outbox row. Commit.
>
> Outside the transaction — deliberately — the relay publishes `OrderPlaced`. Notification service sends an SMS. Fulfilment service routes to the right distributor adapter. Analytics consumes the same event.
>
> **No third-party network calls inside the transaction.** If a distributor's API hangs for 30 seconds I'm not holding database locks for 30 seconds."

**Minute 21–30: Failure modes — budget for this.**

> "**Two pods, same request, same millisecond.** The idempotency insert — the unique constraint decides, not application code. An application-level check-then-insert is a race.
>
> **Phone loses connection after tapping.** Client retries with the same key, finds the row, gets the stored response. One order.
>
> **Two retailers want the last 5 cases.** The conditional update affects one row or zero. Second one fails cleanly. No negative stock.
>
> **Payment fails after the order exists.** The reservation expires and a background job releases it. The order moves to `payment_failed`. The ledger shows an authorisation and a reversal, not a mutation.
>
> **Distributor can only supply half.** Order goes to partially-fulfilled, quantity_confirmed is set per line, retailer is notified, the ledger only reflects what shipped.
>
> **Relay crashes after publishing, before marking sent.** The event publishes twice, which is fine because consumers are idempotent on event ID. At-least-once delivery plus idempotent consumers gives effectively-once processing — you can't get exactly-once across a network.
>
> **The cleanup job for expired reservations dies.** Stock stays locked and nobody notices. So that job needs a metric and an alert on reservations older than their expiry."

**Minute 30+: Scaling, briefly.**

> "Read replicas for order history and catalog, with reads routed to the primary for a few seconds after a retailer's own write so they see their own order. Partition `orders` by month for query speed and cheap archival. Cache the catalog and resolved price lists. **I would not shard** — at this volume it's premature and it's a one-way door. The trigger would be the write rate approaching what one primary can take."

## 12.2 "A brand wants a flash sale — 10x traffic for one hour"

**The shape of a good answer:**

> "First, what kind of 10x? 10x browsing is a completely different problem from 10x orders on one SKU. Browsing is a read problem I solve with caching. 10x orders on a single SKU is a write contention problem on one inventory row, which is much harder.
>
> Assuming it's both: the read side is the easy half. Pre-warm the cache before the sale starts so I don't get a stampede the moment it opens, raise TTLs, make sure the sale landing page is a single cached read, and put jitter on expiry so keys don't all drop together.
>
> The write side is the interesting part. All orders contend on one inventory row, which serialises everything. Options: split that SKU's stock into buckets and pick one at random — faster, but you can report 'sold out' while a bucket still has stock. Or put a queue in front, accept the order as 'submitted' and confirm asynchronously — which is what ticketing systems do and which changes the user experience, so it's a product decision, not just mine to make. Or just let it serialise and check the actual number: if we're selling 5,000 units over an hour, that's two writes a second and the row lock is completely fine.
>
> **I'd do that arithmetic first, because the third option is probably the answer and it's free.**
>
> The other things: a promotion budget counter that stops the sale when exhausted — same race condition as inventory, same fix, a conditional update. Rate limits that don't punish legitimate retry behaviour. And load shedding, so that if we do go over capacity we reject cleanly with a 429 instead of collapsing — a bounded queue degrades, an unbounded one dies."

**Why this answer scores:** it splits the problem, it questions the premise, it does the math, it offers three options with costs, it flags one as a product decision rather than a technical one, and it names the failure mode of the thing it recommends.

## 12.3 "Our retailers order once and don't come back. Fix it."

> "First — do we know where they drop? Registered but never ordered, ordered once and stopped, or ordering less over time are three different problems with three different fixes. Can I assume it's the second?
>
> My leading hypothesis would be **fill rate**. In B2B grocery, if a retailer orders 20 items and gets 12, they go back to their old distributor and don't come back. It's a supply problem that presents as a retention problem. I'd check that first because it's a cheap query — compare first-order fill rate for retailers who came back against those who didn't.
>
> Other hypotheses, roughly in order of how cheap they are to check: delivery time against what we promised; search queries returning nothing, which tells us the catalog is missing what they need; price versus their local alternative; and app drop-off by device tier, because if the app is unusable on a cheap phone nothing else matters.
>
> If fill rate is the problem, the fix isn't a feature — it's supply. Engineering's contribution is making availability honest: don't show items we can't actually deliver, surface substitutes at order time rather than silently short-shipping, and give the retailer the choice. Being honest about availability lowers GMV this week and raises retention this quarter. **That's a trade the business has to agree to, so I'd bring the numbers rather than decide alone.**
>
> If it turns out to be something softer, the cheapest interventions first: a reorder button pre-filled with their last order, a reminder timed to their own restocking cycle, and 'notify me when back in stock' so a stockout becomes captured intent instead of a lost customer.
>
> And I'd ship any of it to 10% with a holdout and measure 30-day repeat rate, because otherwise we won't know if it worked."

**Why this answer scores:** it asks before building, it has a domain-specific leading hypothesis, it ranks by cost of checking, it separates the engineering contribution from the business problem, it names an uncomfortable trade-off honestly, and it ends with measurement.

---

# Part 13 — Rapid-fire bank

Cover the answer, say yours out loud, then check.

**Why Postgres over Mongo here?** Commerce has invariants — stock can't go negative, order total must match line items. I want the database enforcing those, not every piece of application code. `jsonb` covers the semi-structured cases.

**When would you shard?** When one primary's write capacity or one machine's disk is the actual limit. Not before — it's a one-way door that costs cross-shard joins and transactions.

**How do you stop overselling?** A conditional update that affects one row or zero: `UPDATE inventory SET available = available - qty WHERE sku_id = ? AND available >= qty`. Never read-then-check-then-write.

**Why not cache inventory?** Because a stale count causes overselling. Approximate for display is fine; the number checked at commitment comes from the source of truth inside the transaction.

**How do you make an API idempotent?** Client-supplied key per logical intent, unique constraint in the database, `INSERT ... ON CONFLICT DO NOTHING` to decide the winner, return the stored response on a duplicate.

**Can you guarantee exactly-once delivery?** No — it's impossible across a network. You build at-least-once delivery plus idempotent consumers, which gives effectively-once processing.

**How do you publish an event and save to the database atomically?** Transactional outbox. Both rows in one local transaction; a relay publishes from the outbox and marks sent.

**What breaks with read replicas?** Read-your-writes. A retailer who just ordered must see the order, so that read goes to the primary for a short window after their write.

**How do you invalidate a cache?** TTL with a defensible window, delete-on-write with a short TTL as a backstop against the resurrection race, or versioned keys. Name the race: a reader can write a stale value into the cache after the writer deleted it.

**What's a cache stampede and how do you stop it?** A hot key expires and everything misses at once. Jittered TTLs, a single-flight lock, or stale-while-revalidate.

**How do you do a zero-downtime migration?** Expand/contract. Add nullable, backfill in batches, deploy code writing both and reading new, then drop old. A rename is three deploys.

**How do you prevent cross-tenant data leaks?** Row-Level Security in Postgres so the database enforces it, a mandatory data-access layer that injects the filter, tenant from the signed token never a client header, and tests that assert tenant A can't read tenant B.

**What's the difference between partitioning and sharding?** Partitioning splits a table inside one database — you keep joins and transactions. Sharding splits across databases — you lose them.

**Fan-out on write or read for a feed?** Hybrid. Write for normal accounts, read for the few with huge followings.

**How do you handle a distributor's API being down?** Per-partner timeout, retries with backoff and jitter, circuit breaker to fail fast, queue the work for later, and reconcile afterwards.

**Why is a timeout the hardest failure?** Because it's ambiguous — you can't tell "never arrived" from "processed but the response was lost." That ambiguity is why retries exist, why duplicates exist, and why idempotency is mandatory.

**What do you alert on?** Symptoms users feel — error rate, latency percentiles — plus business metrics like orders per minute. Not CPU. A deploy that returns 200 with an empty catalog looks perfectly healthy on infrastructure dashboards.

**Floating point for money?** Never. Integer paise or `NUMERIC`. 0.1 isn't exactly representable in binary floating point and the errors accumulate into reconciliation breaks.

**What goes inside the order transaction?** Idempotency row, price resolution, credit check, inventory reservation, order and lines, outbox row. **No third-party network calls.**

**When would you use Kafka here?** When several independent consumers need the same event stream, or when I want replay. Not for throughput at one order per second — a Postgres queue with `FOR UPDATE SKIP LOCKED` handles that with no new infrastructure.

---
