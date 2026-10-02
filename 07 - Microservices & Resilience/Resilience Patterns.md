---
aliases: [Circuit Breaker, Circuit Breaking Concepts, Retry Pattern, Timeout Pattern, Fallback Pattern, Bulkhead Pattern]
---
# Resilience Patterns

> Five patterns that only work as a set. A call fails → timeout bounds the wait → retry handles the blip → the breaker gives up → fallback degrades gracefully → the bulkhead stops it spreading.

## Timeout
<!-- never wait forever. An unbounded call holds a thread and the failure propagates upstream. Set it before anything else. -->

## Retry
<!-- for transient failures only. See [[Retry Strategies, Backoff & Jitter]] for backoff and jitter — the retry itself is the easy part. -->

## Circuit Breaker
<!-- closed → open → half-open. After N failures, stop calling and fail fast; probe occasionally to see if it recovered. Stops retries hammering a dead service. -->

## Fallback
<!-- what you return when the breaker is open: cached value, default, degraded feature. Decide this per call site. -->

## Bulkhead
<!-- isolate resources (thread pools, connection pools) per dependency so one slow service cannot exhaust everything. -->

## How they compose
<!-- timeout + retry + breaker + fallback on one call, bulkheads around the whole dependency. Retry without a breaker is a self-inflicted DDoS. -->

---
## 🔗 Connections
- **Prerequisite:** [[Retry Strategies, Backoff & Jitter]] [[Failure Handling]]
- **Used by / relates to:** [[Idempotency]] [[Dead Letter Queues & Poison Messages]] [[Cache Failure Modes]] [[Health Probes]]
- **Applied in:** [[API Gateway & BFF]] [[Payment Gateway]]

#microservices #resilience #review
