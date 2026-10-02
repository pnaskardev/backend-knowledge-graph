---
aliases: [Cache Aside, Write Through, Write Behind, Refresh Ahead]
---
# Caching Patterns

> Four ways to wire a cache to the database. Learn them as one table of trade-offs.

## Cache Aside (lazy loading)
<!-- app checks cache, misses, reads DB, populates. The default. -->

## Write Through
<!-- write to cache and DB together. Consistent, slower writes. -->

## Write Behind (write back)
<!-- write to cache, flush to DB async. Fast writes, risk of data loss. -->

## Refresh Ahead
<!-- refresh hot keys before they expire, so nobody ever hits a miss. -->

## Key trade-off
<!-- consistency vs write latency vs complexity. One row per pattern. -->

---
## 🔗 Connections
- **Prerequisite:** [[Redis]]
- **Used by / relates to:** [[Cache Invalidation]] [[Cache Failure Modes]] [[Distributed Cache]]
- **Contrast with:** [[Outbox & Inbox Patterns]]

#caching #pattern #review
