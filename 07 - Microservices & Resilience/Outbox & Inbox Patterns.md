---
aliases: [Transactional Outbox, Inbox Pattern]
---
# Outbox & Inbox Patterns

> Two halves of one problem: the producer must not lose an event, the consumer must not process it twice.

## The dual-write problem
<!-- write to the DB and publish to the broker — if the second fails you are inconsistent. No distributed transaction is available. -->

## Transactional Outbox (producer side)
<!-- write the event into an outbox table in the same DB transaction. A relay polls the table and publishes. Atomic, because it is one transaction. -->

## Inbox Pattern (consumer side)
<!-- record processed message IDs in an inbox table; skip anything already seen. This is [[Idempotency]] made durable. -->

## Why you need both
<!-- the outbox gives at-least-once delivery, so the inbox is what turns that into effectively-once processing. -->

---
## 🔗 Connections
- **Prerequisite:** [[Transactions & Concurrency Control]] [[Idempotency]]
- **Used by / relates to:** [[SAGA Pattern]] [[Event-Driven Architectures]] [[Message Queue Fundamentals]]
- **Contrast with:** [[Exactly Once vs At Least Once vs At Most Once]]

#microservices #review
