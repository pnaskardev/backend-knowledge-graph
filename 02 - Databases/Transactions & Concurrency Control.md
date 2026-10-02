---
aliases: [Transactions, Isolation Levels, MVCC, Optimistic Locking, Pessimistic Locking]
---
# Transactions & Concurrency Control

> One chain: a transaction promises isolation → isolation levels define how much → MVCC and locking are how engines deliver it.

## Transactions
<!-- unit of work, commit/rollback. ACID is the promise. -->

## Isolation Levels
<!-- Read Uncommitted → Read Committed → Repeatable Read → Serializable, and the anomaly each one allows (dirty read, non-repeatable read, phantom). -->

## MVCC
<!-- keep multiple versions so readers never block writers. How Postgres/InnoDB implement the levels above. -->

## Optimistic Locking
<!-- no lock; version/timestamp check at commit, retry on conflict. Good for low contention. -->

## Pessimistic Locking
<!-- take the lock up front. Good for high contention, costs throughput and risks deadlock. -->

## Key trade-off
<!-- stronger isolation = less concurrency. Pick the weakest level your correctness actually needs. -->

---
## 🔗 Connections
- **Prerequisite:** [[ACID vs BASE]]
- **Used by / relates to:** [[Indexing]] [[Distributed Locking]]
- **Contrast with:** [[SAGA Pattern]] [[Consistency Models]]

#databases #concurrency #review
