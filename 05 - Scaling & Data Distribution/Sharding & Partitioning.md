---
aliases: [Sharding, Partitioning]
---
# Sharding & Partitioning

> Sharding is partitioning spread across machines. Same idea, different blast radius.

## Partitioning
<!-- split one table/dataset into chunks. Can be within a single node. -->

## Sharding
<!-- those partitions live on separate machines. Now every cross-shard query is a distributed query. -->

## Choosing a shard key
<!-- range vs hash. Hot keys and skew are the thing that actually bites you. -->

## Rebalancing
<!-- what happens when you add a node — this is why [[Consistent Hashing]] exists. -->

## Key trade-off
<!-- write/storage scale, at the cost of cross-shard joins, transactions, and rebalancing pain. -->

---
## 🔗 Connections
- **Prerequisite:** [[Indexing]] [[Consistent Hashing]]
- **Used by / relates to:** [[Replication]] [[Distributed Cache]] [[Kafka]]
- **Contrast with:** [[DynamoDB-style Stores]]

#scaling #review
