---
aliases: [Topic, Partition, Offset, Consumer Groups, Kafka Replay]
---
# Kafka

> A distributed, partitioned, replayable log. Topic → partition → offset is the whole mental model; everything else follows from it.

## Topic & Partition
<!-- a topic is split into partitions; a partition is an append-only ordered log. Ordering is per-partition only, never across a topic. -->

## Offset
<!-- the consumer's position in a partition. The broker does not track "done" — the consumer commits its offset. -->

## Consumer Groups
<!-- one partition goes to exactly one consumer in a group. So group parallelism is capped by partition count. -->

## Kafka Replay
<!-- messages are not deleted on read; reset the offset and reprocess history. This is what makes Kafka different from a queue. -->

## Retention & the log
<!-- time or size based. Why Kafka is a log, not a queue. -->

## Key trade-off
<!-- huge throughput and replay, at the cost of per-partition ordering and offset management on the consumer. -->

---
## 🔗 Connections
- **Prerequisite:** [[Message Queue Fundamentals]] [[Sharding & Partitioning]]
- **Used by / relates to:** [[Message Ordering]] [[Schema Evolution & Event Versioning]] [[Backpressure]] [[Replication]]
- **Contrast with:** [[RabbitMQ]] [[Kafka vs RabbitMQ]]

#messaging #kafka #review
