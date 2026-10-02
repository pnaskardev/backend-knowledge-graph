---
aliases: [Message Queue, Queue, Producer, Consumer, Point to Point Messaging, Publish Subscribe]
---
# Message Queue Fundamentals

> Producer, queue, consumer — one picture. The only real decision is point-to-point vs publish-subscribe.

## The pieces
<!-- Producer writes, Queue buffers, Consumer reads. The queue is what decouples them in time. -->

## Point to Point
<!-- one message, one consumer. Work distribution — competing consumers share the load. -->

## Publish Subscribe
<!-- one message, every subscriber gets a copy. Event broadcast, not work distribution. -->

## Push vs pull
<!-- broker pushes to the consumer (RabbitMQ) vs consumer pulls at its own pace (Kafka). Decides who handles [[Backpressure]]. -->

## Acknowledgement
<!-- when does the broker consider a message done? This is where delivery guarantees come from. -->

## Key trade-off
<!-- decoupling and buffering, paid for with an extra moving part, ordering problems, and duplicate delivery. -->

---
## 🔗 Connections
- **Prerequisite:** [[Event-Driven Architectures]]
- **Used by / relates to:** [[RabbitMQ]] [[Kafka]] [[Dead Letter Queues & Poison Messages]] [[Backpressure]] [[Message Ordering]]
- **Contrast with:** [[Exactly Once vs At Least Once vs At Most Once]]

#messaging #review
