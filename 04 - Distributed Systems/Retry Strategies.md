# Retry Strategies

**One-liner:** Whenever a request fails we try again in some time with a default backoff, this is a very basic retry mechanism.

This is very basic and only useful for systems where traffic is really less.

**Why / when it's used:** 
	Used in very basic systems where the microservice traffic is less
**Key trade-off:** 
	the microservice may be down for a long time and you have 10000 clients, if you start retrying at the same time all the clients keep on retrying at regular intervals, that basically means the server is down and the instance gets 10K request at the same time there is no point in hammering the instance with all these requests maybe let the server come back up.

---
## 🔗 Connections
- **Prerequisite:** [[Idempotency]] [[Failure Handling]]
- **Used by / relates to:** [[Exponential Backoff]] [[Jitter]] [[Circuit Breaking Concepts]] [[Retry Pattern]]
- **Applied in:** [[Message Queue]] [[Distributed Cache]]

#reliability #distributed-systems #review
