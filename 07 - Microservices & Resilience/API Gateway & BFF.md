---
aliases: [API Gateway, Backend for Frontend (BFF)]
---
# API Gateway & BFF

> One entry point for clients. A BFF is just an API gateway specialised per client type.

## API Gateway
<!-- single front door: routing, auth, rate limiting, TLS termination, aggregation. Keeps cross-cutting concerns out of every service. -->

## Backend for Frontend
<!-- one gateway per client (web, mobile, partner), each shaping responses for that client's needs instead of one lowest-common-denominator API. -->

## When BFF beats a single gateway
<!-- when mobile needs fewer fields and fewer round trips than web, and a shared API makes both worse. -->

## Key trade-off
<!-- a gateway is a single point of failure and a deployment bottleneck. A BFF per client multiplies the code you maintain. -->

---
## 🔗 Connections
- **Prerequisite:** [[Load Balancer]] [[API Design]]
- **Used by / relates to:** [[Service Discovery]] [[Authentication & Authorization]] [[Rate Limiting Algorithms]] [[Resilience Patterns]]
- **Contrast with:** [[Sidecar, Ambassador & Adapter Patterns]]

#microservices #review
