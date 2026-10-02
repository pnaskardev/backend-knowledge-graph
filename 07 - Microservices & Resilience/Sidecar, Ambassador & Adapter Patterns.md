---
aliases: [Sidecar Pattern, Ambassador Pattern, Adapter Pattern (Deployment)]
---
# Sidecar, Ambassador & Adapter Patterns

> Three names for the same move: put a helper container next to your service instead of code inside it. They differ only in what the helper does.

## Sidecar
<!-- the general case. A co-deployed container sharing the pod's lifecycle and network — logging, config, proxying. -->

## Ambassador
<!-- a sidecar that handles outbound calls: retries, TLS, service discovery. The app just calls localhost. -->

## Adapter
<!-- a sidecar that normalises outbound data: turns the app's metrics/logs into the format the platform expects. -->

## Why bother
<!-- cross-cutting concerns in one place, in any language, without touching the service. This is how a service mesh works. -->

## Key trade-off
<!-- an extra container per pod: more memory, another network hop, another thing to debug. -->

---
## 🔗 Connections
- **Prerequisite:** [[Pod]] [[Containers & Docker]]
- **Used by / relates to:** [[Service Discovery]] [[Resilience Patterns]] [[API Gateway & BFF]]

#microservices #deployment #review
