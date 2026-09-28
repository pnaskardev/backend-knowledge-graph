Think about a situation where you have are maintaining an e-commerce site. A customer clicks Pay on your checkout page.

The loader takes 10 seconds then an error message pops up and says "Something went wrong. Please try again."

They click Pay button again and this time it works. Now after two days later they email the support team angrily because their bank statement shows two charges.

Every service did what it was written to do. The payment provider charged the card the first time, the response just never made it back before your server gave up waiting. The code saw an error and reported one. The customer did a reasonable thing and retried.

The failure wasn't a single component.

This article walks through the ideas that matter, from the mental model up to the patterns you'll use daily.

## Failure is the normal case

The first thing we need to understand is that we need to stop treating failure as an exception. In a distributed system at scale some thing is was always broken somewhere.

At scale rare events happen everyday.

## Timeouts: deciding when to stop waiting

Every call across a network needs a timeout. Without one a hung network call will accumulate blocked requests until the server runs out of connections or memory and eventually crashes.

Choosing the value is a judgement call from the developers side. Too short and we will abandon requests which would have succeeded, turning normal slowness into errors.

Too long and we block resources unnecessarily.

## Retries: The obvious fix and its hidden danger

This is the most obvious response to a failure is to try again. Networks partition, node restart, and a second attempt usually succeeds.

But here is the catch we are supposed to retry whats safe to repeat, for example - Retry a read is harmless and nothing will escalate, but retry charging a card without protection will cause a lot of problems later.

In the next section we will see how idem-potency can be utilized while retrying.

### How to retry

Back off and jitter, if a service fails each an every client will start retrying immediately and at scale the retries will add load at the worst moment.

Exponential Back off gives time to the service and spaces out the retry attempts to recover; wait out for 100 ms, then 200 ms, then 400 ms.

But Exponential back-off isn't enough on its own, consider a situation where thousands of clients are connected to a service and all of them start retrying after 100 ms then after 200 ms, this will cause event storming and system will crash again even after retrying.

```go
func retry(ctx context.Context, attempts int, base, max time.Duration,
    op func(context.Context) error) error {

    var err error
    for i := 0; i < attempts; i++ {
        if err = op(ctx); err == nil || !isRetryable(err) {
            return err
        }
        backoff := base << i
        if backoff > max {
            backoff = max
        }
        wait := time.Duration(rand.Int63n(int64(backoff))) // "full jitter"
        select {
        case <-time.After(wait):
        case <-ctx.Done():
            return ctx.Err() // caller gave up; stop wasting work
        }
    }
    return err
}
```

## Idem-potency - making a retry safe

First we need to understand what is an idem-potent event.

Any operation is idem-potent only and only if doing it twice has the same result as doing it once.

The standard key is \`idempotency\_key\`. The client generates an idempotency key and sends it with every request, the server records the key along with the result. If the same key shows up again, the server returns the stored result instead of doing some work on it. Payment gateways like Stripe expose exactly this, and well-designed internal APIs do too.

The naive approach to implement this is "check whether the key exists, and if not, insert it," has a race: two retries arriving simultaneously both see "doesn't exist" and both proceed. The fix is to let the database enforce uniqueness atomically:

```sql
INSERT INTO processed_events (event_id, order_id, payload)
VALUES ($1, $2, $3)
ON CONFLICT (event_id) DO NOTHING;
-- 0 rows affected => we've seen this event before; acknowledge and stop
```

## The dual write problem

Any well designed micro service does two things :-

*   Update the order in the database
    
*   then publish and \`\`\`order.paid\`\`\` event to the Kafka broker so that other services for example(invoicing, notifications) can react and do their own specific job.
    

Now we need to think that what if process crashes between these tow steps?

The Database will reflect that the order has been paid but other services were never notified through the event.

We can't make the database write and Kafka publish atomic, since both of them are separate systems and the code level database transaction block has no control over the Kafka systems.

The standard solution is something called \`\`\`transactional outbox\`\`\` and the intuition behind it is that make the event part of the database write.

In the same transaction as the business change, insert a row into an outbox table. A separate process reads the unsent outbox rows and publishes them, marking each one sent.

Even after the process crashes, when the system recovers the separate relay process is spawned which just checks the last unsent message and starts publishing from the last checkpoint.

### Reconciliation

Idem-potency prevents damage when an event occurs twice but what will happen if the event never occurred, this may seem a very far fetched idea but this case is actually very common for example -

Your web-hook was sent to an URL that was down for some maintenance. The sender process crashed after calling the gateway and did not have a record of the last event it tried sending.

The solution is to simply add a job that closes the loop. It selects orders with a non-terminal state and longer than some threshold, ask the provider what actually happened with the particular event and then drive the event through the same idempotent transitions that it would have used when healthy.

The provider's API is the source of truth, not your database. That is the whole idea.

### What should we do when the worker spans services

A single transaction block can protect one database but it cannot protect a flow which reserves the slot in one service, charge the payment gateway in a separate service and start the session in a separate service.

There are mainly 2 ways of handling such situations -

*   2 Phase Commit
    
    *   They hold locks across services and turn any coordinator into a system stall.
        
*   SAGA Pattern [Read more in here](https://priyanshucodes.hashnode.dev/sagas-to-maintain-data-consistency-in-a-microservice-architecture).
    
    *   The practical solution is to breaking the flow into multiple local transactions, each with a compensating actions as well.
        
    *   If any of the local transactions fail we run a compensating action for the steps which are failed and then voila we have a consistent database.

---
## 🔗 Connections
- **Prerequisite:** [[Distributed Systems Trade-offs]]
- **Used by / relates to:** [[Retry Strategies, Backoff & Jitter]] [[Circuit Breaking Concepts]] [[Bulkhead Pattern]] [[Timeout Pattern]]
- **Applied in:** [[Payment Gateway]]

#distributed-systems #review
