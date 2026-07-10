# 📚 STUDY PLAN — Backend / System Design for SDE-1 & SDE-2

The one file that answers **"what do I study after what?"** Work top to bottom. Each `[[link]]` is a note you fill in **your own words** (a one-liner, why it's used, the key trade-off, one recall question). A topic can grow into a full article whenever you want — there's no template to follow.

> New here? Read [[How to study fast]] and [[How to Drill (Interview Mode)]] first — they take 3 minutes and define the method below.

## How to use this plan
- **Breadth first, then depth.** Fill every note in a phase with a quick definition + trade-off before going deep on any one. Interviews reward coverage + trade-offs, not perfection.
- **Active recall.** Every note ends with `#review`. Once you can explain a topic *out loud without looking*, change its tag to `#solid`. Your daily job is to shrink the `#review` pile.
- **~5 min per note.** Don't polish. Move on. Come back when it's a `#review` you keep getting wrong.
- **Suggested pace:** 15–25 notes/day within a single phase, then one recall pass over that phase's `#review` notes before starting the next phase.
- **Check a box** when a note is at `#solid`.

## 🔑 Cross-cutting, highest-leverage topics
These show up in almost every system design answer. Get them solid early (they live in phases 2–5):
[[Consistency Models]] · [[Idempotency]] · [[Retry Strategies]] · [[Sharding]] · [[Replication]] · [[Consistent Hashing]] · [[Distributed Cache]]

---

## Phase 0 — Start Here (read, don't drill)
- [ ] [[00 - Home]]
- [ ] [[How to study fast]]
- [ ] [[How to Drill (Interview Mode)]]

## Phase 1 — Web & Networking Basics
*The request's journey before it hits your service. Short phase, foundational vocabulary.*
- [ ] [[API Design]]  — REST vs gRPC vs GraphQL, versioning, pagination
- [ ] [[Load Balancer]]  — L4 vs L7, algorithms, health checks
- [ ] [[CDN]]  — edge caching, when it helps
- [ ] [[WebSockets-style Connections]]  — persistent/bidirectional vs request-response
- [ ] [[Authentication & Authorization]]  — sessions, JWT, OAuth basics

## Phase 2 — Databases
*Prereq for caching, scaling, and every system design. Do this before Phase 5.*
- **Basics:** [ ] [[ACID]] · [ ] [[BASE]] · [ ] [[SQL vs NoSQL]] · [ ] [[DynamoDB-style Stores]]
- **Indexing & storage:** [ ] [[B+ Trees]] · [ ] [[Clustered Index]] · [ ] [[Secondary Index]] · [ ] [[Composite Index]] · [ ] [[Covering Index]]
- **Concurrency:** [ ] [[Transactions]] · [ ] [[Isolation Levels]] · [ ] [[MVCC]] · [ ] [[Optimistic Locking]] · [ ] [[Pessimistic Locking]]
- Hub: [[Databases MOC]]

## Phase 3 — Caching
*Make reads fast. Builds on Databases.*
- **Fundamentals:** [ ] [[Redis]] · [ ] [[Distributed Cache]]
- **Write/read patterns:** [ ] [[Cache Aside]] · [ ] [[Write Through]] · [ ] [[Write Behind]] · [ ] [[Refresh Ahead]]
- **Failure modes:** [ ] [[Cache Invalidation]] · [ ] [[Cache Stampede]] · [ ] [[Cache Avalanche]] · [ ] [[Cache Penetration]]
- Hub: [[Caching MOC]]

## Phase 4 — Distributed Systems Fundamentals
*The mental models for many-machine systems. The heart of SDE-2 interviews.*
- **Models & trade-offs:** [ ] [[CAP Theorem]] · [ ] [[PACELC]] · [ ] [[Consistency Models]] · [ ] [[Distributed Systems Trade-offs]]
- **Time & failure:** [ ] [[Clock Synchronization]] · [ ] [[Failure Handling]]
- **Coordination & consensus:** [ ] [[Consensus Algorithms]] · [ ] [[Leader Election]] · [ ] [[Distributed Locking]] · [ ] [[Split Brain]] · [ ] [[Quorum Reads and Writes]]
- **Reliability primitives:** [ ] [[Idempotency]] · [ ] [[Retry Strategies]] · [ ] [[Exponential Backoff]] · [ ] [[Jitter]] · [ ] [[Circuit Breaking Concepts]] · [ ] [[Exactly Once vs At Least Once vs At Most Once]]
- Hub: [[Distributed Systems MOC]]

## Phase 5 — Scaling & Data Distribution
*How you grow a system. Needs Databases + Distributed Systems first.*
- [ ] [[Replication]] · [ ] [[Read Replicas]] · [ ] [[Sharding]] · [ ] [[Partitioning]] · [ ] [[Consistent Hashing]] · [ ] [[Rate Limiting Algorithms]]

## Phase 6 — Messaging & Streaming
*Async communication. Underpins microservices and event-driven designs.*
- **Fundamentals:** [ ] [[Event Driven Architecture]] · [ ] [[Message Queue]] · [ ] [[Publish Subscribe]] · [ ] [[Point to Point Messaging]]
- **RabbitMQ:** [ ] [[RabbitMQ]] · [ ] [[Exchange]] · [ ] [[Queue]] · [ ] [[Binding]] · [ ] [[Routing Key]] · [ ] [[Direct Exchange]] · [ ] [[Fanout Exchange]] · [ ] [[Topic Exchange]] · [ ] [[Headers Exchange]] · [ ] [[Dead Letter Queue]] · [ ] [[Poison Messages]]
- **Kafka:** [ ] [[Kafka]] · [ ] [[Topic]] · [ ] [[Partition]] · [ ] [[Producer]] · [ ] [[Consumer]] · [ ] [[Consumer Groups]] · [ ] [[Offset]] · [ ] [[Kafka Replay]]
- **Advanced:** [ ] [[Kafka vs RabbitMQ]] · [ ] [[Message Ordering]] · [ ] [[Backpressure]] · [ ] [[Event Versioning]] · [ ] [[Schema Registry]]
- Hub: [[Messaging MOC]]

## Phase 7 — Microservices & Resilience Patterns
*Composing services. Pulls together Databases, Messaging, and Distributed Systems.*
- **Service design:** [ ] [[Database per Service]] · [ ] [[API Gateway]] · [ ] [[Service Discovery]] · [ ] [[Backend for Frontend (BFF)]]
- **Communication & data consistency:** [ ] [[SAGA Pattern]] · [ ] [[CQRS]] · [ ] [[Event-Driven Architectures]] · [ ] [[Transactional Outbox]] · [ ] [[Inbox Pattern]]
- **Resilience:** [ ] [[Circuit Breaker]] · [ ] [[Bulkhead Pattern]] · [ ] [[Retry Pattern]] · [ ] [[Timeout Pattern]] · [ ] [[Fallback Pattern]]
- **Deployment & migration:** [ ] [[Sidecar Pattern]] · [ ] [[Ambassador Pattern]] · [ ] [[Adapter Pattern (Deployment)]] · [ ] [[Strangler Pattern]] · [ ] [[Database Migration Patterns]]
- Hub: [[Microservices MOC]]

## Phase 8 — Kubernetes & Deployment
*How services run in production. Independent — can be done any time after Phase 1.*
- **Containers:** [ ] [[Docker]] · [ ] [[Container]]
- **Core objects:** [ ] [[Kubernetes]] · [ ] [[Pod]] · [ ] [[Deployment]] · [ ] [[ReplicaSet]] · [ ] [[Service]] · [ ] [[Ingress]]
- **Configuration:** [ ] [[ConfigMap]] · [ ] [[Secret]]
- **Scaling & health:** [ ] [[Horizontal Pod Autoscaler]] · [ ] [[Liveness Probe]] · [ ] [[Readiness Probe]]
- Hub: [[Kubernetes MOC]]

## Phase 9 — Low Level Design (OOP)
*Object modelling. Mostly independent; foundations first, then problems easy → hard.*
- **Foundations:** [ ] [[SOLID Principles]] · [ ] [[Design Patterns]]
- **Problems:** [ ] [[Parking Lot]] · [ ] [[Logger]] · [ ] [[ATM]] · [ ] [[Elevator]] · [ ] [[Splitwise]] · [ ] [[Cache (LLD)]] · [ ] [[BookMyShow]] · [ ] [[Food Delivery]] · [ ] [[Chess]]
- Hub: [[Low Level Design MOC]]

## Phase 10 — System Design Case Studies (do these LAST)
*Apply everything. For each: sketch your own design on paper first, then compare against the "Uses these concepts" links — the gap is your study list.*
- **Beginner:** [ ] [[URL Shortener]] · [ ] [[Pastebin]] · [ ] [[Rate Limiter]]
- **Intermediate:** [ ] [[Notification Service]] · [ ] [[Distributed Cache (System Design)]] · [ ] [[Search Engine]] · [ ] [[File Storage]]
- **Advanced:** [ ] [[Chat Application]] · [ ] [[News Feed]] · [ ] [[Ride Sharing]] · [ ] [[Payment Gateway]] · [ ] [[Video Streaming]]
- Hub: [[System Design MOC]]

---

### Two-track advice
- **SDE-1:** Phases 1–3, the reliability primitives in Phase 4, Phase 9, and the Beginner/Intermediate cases in Phase 10 will carry most interviews.
- **SDE-2:** All of Phase 4–7 solid, plus Advanced cases in Phase 10. Expect deep trade-off follow-ups.

#moc
