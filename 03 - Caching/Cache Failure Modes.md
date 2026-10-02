---
aliases: [Cache Stampede, Cache Avalanche, Cache Penetration]
---
# Cache Failure Modes

> Three ways a cache turns into a DB outage. Same shape: traffic that should have been absorbed hits the database instead.

## Cache Stampede (thundering herd)
<!-- one hot key expires, N concurrent requests all miss and all hit the DB. Fix: lock/single-flight, or jittered TTL. -->

## Cache Avalanche
<!-- many keys expire at once (same TTL, or the cache restarts). Fix: jitter the TTLs. -->

## Cache Penetration
<!-- requests for keys that do not exist anywhere, so the cache never helps. Fix: cache the negative result, or a bloom filter. -->

## The common fix
<!-- jitter, single-flight, and never let a miss go straight to the DB unthrottled. -->

---
## 🔗 Connections
- **Prerequisite:** [[Caching Patterns]] [[Retry Strategies, Backoff & Jitter#Jitter|Jitter]]
- **Used by / relates to:** [[Cache Invalidation]] [[Distributed Cache]]
- **Contrast with:** [[Resilience Patterns]]

#caching #problem #review
