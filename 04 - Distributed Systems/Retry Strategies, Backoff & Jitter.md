# Retry Strategies, Backoff & Jitter

**One-liner:** When a request fails, try again after a delay — how you pick that delay is the whole topic.

**Why / when it's used:** Transient failures (a restarting instance, a brief network blip, a timeout) succeed on a second attempt. Retrying is the cheapest way to survive them.

**Key trade-off:** Retries turn one failure into many requests. Done naively, they hammer a service that is already struggling and turn a blip into an outage.

---
## Fixed retry

Retry on a constant interval. Fine when traffic is low.

The problem: the service is down for a while and you have 10,000 clients. Every client retries on the same fixed interval, so the instance gets 10,000 requests every cycle while it is trying to come back up. There is no point hammering it — let it recover.

## Exponential Backoff

Instead of a constant interval, grow the delay exponentially — 1s, 2s, 4s, 8s. Each failure buys the instance more room to recover.

`delay = base * 2^attempt`, usually with a `max_delay` cap and a max attempt count.

Still broken: if all 10,000 clients failed **together**, they all back off by the same amounts and so they all retry together. The spike is delayed, not spread. Same thundering herd, just later.

## Jitter

Add randomness to the backoff so clients spread out instead of retrying in lockstep.

- **Full jitter:** `delay = random(0, base * 2^attempt)` — best spread, the usual default.
- **Equal jitter:** `delay = half + random(0, half)` where `half = base * 2^attempt / 2` — keeps a minimum backoff while still spreading.

Jitter is what actually breaks the synchronised herd. Exponential backoff without jitter only moves the spike.

## What to pair retries with

- **[[Idempotency]]** — a retry may hit a request that actually succeeded. Without idempotency you get duplicates.
- **[[Circuit Breaking Concepts]]** — retries alone never give up. A breaker stops the retrying once the service is clearly down.
- **Retry budget / max attempts** — always cap. Unbounded retries are a self-inflicted DDoS.
- **Only retry what is retryable** — timeouts and 5xx yes, 4xx no.

---
## 🔗 Connections
- **Prerequisite:** [[Idempotency]] [[Failure Handling]]
- **Used by / relates to:** [[Circuit Breaking Concepts]] [[Retry Pattern]] [[Cache Stampede]]
- **Applied in:** [[Message Queue]] [[Distributed Cache]]

#reliability #distributed-systems #review
