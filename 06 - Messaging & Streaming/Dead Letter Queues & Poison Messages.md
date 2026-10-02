---
aliases: [Dead Letter Queue, Poison Messages]
---
# Dead Letter Queues & Poison Messages

> A poison message is the problem; a dead letter queue is the answer. Never learn one without the other.

## Poison Messages
<!-- a message that fails every time — malformed, or a bug in the consumer. Without a DLQ it is redelivered forever and blocks the queue. -->

## Dead Letter Queue
<!-- after N failed attempts, move it aside instead of retrying. The queue keeps moving; a human inspects the DLQ later. -->

## Setting the retry limit
<!-- too low and you DLQ transient failures; too high and one bad message stalls the consumer. Pairs with [[Retry Strategies, Backoff & Jitter]]. -->

## Operating a DLQ
<!-- it needs an alarm and a replay path, or it is just a place messages go to die. -->

---
## 🔗 Connections
- **Prerequisite:** [[Message Queue Fundamentals]]
- **Used by / relates to:** [[Retry Strategies, Backoff & Jitter]] [[Idempotency]] [[RabbitMQ Exchanges & Routing]]
- **Contrast with:** [[Resilience Patterns]]

#messaging #review
