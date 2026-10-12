# System Design Topics — The Complete Learning List

**For:** Kirana Club SDE 2 Round 2, and system design interviews generally
**Companions:** `kirana_club.md` (fundamentals + resume defence) · `kirana_club_round2.md` (how to run the round, the commerce subsystems, worked examples)

---

## How to use this document

The other two docs teach you how to *answer*. This one is the **topic list** — every building block used to scale a commerce platform like Meesho, Amazon or Kirana Club, each one explained the same way so you can learn them one at a time.

Every topic follows this shape:

- **What it is** — plain words
- **Example** — concrete, usually a kirana store buying Parle-G
- **Pros / Cons**
- **When to use / when not to**
- **Interview line** — the sentence to say

**Topics are tiered. Do not try to learn all of them.**

- **T1 — Must know cold.** You will be asked, or you'll need it to answer something else. About 20 topics. If you only have one day, this is the day's work.
- **T2 — Should be able to discuss.** Likely to come up as a follow-up. Know what it is, the main trade-off, and when you'd reach for it.
- **T3 — Name and move on.** Know the word and one sentence. Enough to say "that's where I'd look," not enough to design it. Trying to go deep here is how people waste prep time.

**Suggested order:** read the tier map below, then do all T1 in order, then T2 for the groups most relevant to commerce (3, 4, 5, 6), then skim T3.

---

## The tier map

| # | Topic | Tier | Group |
|---|---|---|---|
| 1 | DNS and how a request finds your server | T3 | Request path |
| 2 | Load balancers (L4 vs L7) | T1 | Request path |
| 3 | Reverse proxy | T2 | Request path |
| 4 | API gateway | T1 | Request path |
| 5 | Backend-for-Frontend (BFF) | T2 | Request path |
| 6 | CDN and edge caching | T1 | Request path |
| 7 | TLS termination | T3 | Request path |
| 8 | REST API design | T1 | Communication |
| 9 | gRPC and Protobuf | T2 | Communication |
| 10 | GraphQL | T3 | Communication |
| 11 | WebSockets vs SSE vs polling | T2 | Communication |
| 12 | Webhooks | T1 | Communication |
| 13 | Serialization and schema evolution | T2 | Communication |
| 14 | Service discovery | T3 | Communication |
| 15 | Service mesh | T3 | Communication |
| 16 | Storage engines: B-tree vs LSM-tree | T2 | Storage |
| 17 | Write-ahead log (WAL) | T2 | Storage |
| 18 | Indexing | T1 | Storage |
| 19 | Replication | T1 | Storage |
| 20 | Partitioning and sharding | T1 | Storage |
| 21 | Consistent hashing | T2 | Storage |
| 22 | Federation (functional partitioning) | T3 | Storage |
| 23 | Materialised views | T2 | Storage |
| 24 | Object storage | T2 | Storage |
| 25 | Tiered storage and archival | T3 | Storage |
| 26 | Columnar and time-series stores | T2 | Storage |
| 27 | Data warehouse, ETL/ELT | T3 | Storage |
| 28 | Change data capture (CDC) | T2 | Storage |
| 29 | Multi-level caching | T1 | Caching |
| 30 | Cache patterns and invalidation | T1 | Caching |
| 31 | Eviction policies | T2 | Caching |
| 32 | Bloom filters | T3 | Caching |
| 33 | Cache stampede | T1 | Caching |
| 34 | Message queues | T1 | Async |
| 35 | Event streaming (log) | T1 | Async |
| 36 | Pub-sub | T2 | Async |
| 37 | Delivery semantics | T1 | Async |
| 38 | Transactional outbox | T1 | Async |
| 39 | Dead letter queues | T2 | Async |
| 40 | Batch vs stream processing | T2 | Async |
| 41 | Lambda and Kappa architecture | T3 | Async |
| 42 | Backpressure | T2 | Async |
| 43 | Distributed scheduling / cron at scale | T2 | Async |
| 44 | CAP and PACELC | T1 | Consistency |
| 45 | Consistency models | T1 | Consistency |
| 46 | Two-phase commit | T2 | Consistency |
| 47 | Sagas | T1 | Consistency |
| 48 | Idempotency | T1 | Consistency |
| 49 | Distributed locks and fencing tokens | T2 | Consistency |
| 50 | Leader election and consensus (Raft) | T3 | Consistency |
| 51 | Clocks, logical clocks, vector clocks | T2 | Consistency |
| 52 | Distributed ID generation | T2 | Consistency |
| 53 | Timeouts, retries, backoff, jitter | T1 | Reliability |
| 54 | Circuit breaker | T1 | Reliability |
| 55 | Bulkhead | T2 | Reliability |
| 56 | Load shedding and admission control | T2 | Reliability |
| 57 | Rate limiting | T1 | Reliability |
| 58 | Graceful degradation and fallbacks | T1 | Reliability |
| 59 | Health checks: liveness vs readiness | T2 | Reliability |
| 60 | Redundancy, failover, RPO/RTO, backups | T2 | Reliability |
| 61 | Multi-AZ vs multi-region | T2 | Reliability |
| 62 | Chaos engineering | T3 | Reliability |
| 63 | Deployment strategies (blue-green, canary, rolling) | T2 | Operations |
| 64 | Feature flags | T2 | Operations |
| 65 | Expand/contract migrations | T1 | Operations |
| 66 | Autoscaling | T2 | Operations |
| 67 | Capacity planning and load testing | T2 | Operations |
| 68 | Observability: logs, metrics, traces | T1 | Operations |
| 69 | SLI, SLO, error budgets | T2 | Operations |
| 70 | Cost as a design constraint | T2 | Operations |
| 71 | Inverted index and search ranking | T2 | Search & geo |
| 72 | Geospatial indexing | T2 | Search & geo |
| 73 | Recommendations and cold start | T3 | Search & geo |
| 74 | A/B testing infrastructure | T3 | Search & geo |
| 75 | AuthN and AuthZ, JWT, OAuth | T1 | Security |
| 76 | RBAC and ABAC | T2 | Security |
| 77 | Multi-tenancy isolation | T1 | Security |
| 78 | Encryption and PII handling | T2 | Security |
| 79 | DDoS, WAF, bot protection | T3 | Security |
| 80 | **Saga rollback and compensation** | T1 | Deep dives |
| 81 | **Distributed tracing** | T1 | Deep dives |
| 82 | **Distributed logging and correlation** | T1 | Deep dives |
| 83 | **Inventory and stock correctness** | T1 | Deep dives |
| 84 | **Payments, ledger and money movement** | T1 | Deep dives |
| 85 | **Credit, limits and exposure** | T2 | Deep dives |
| 86 | **Flash sale architecture** | T1 | Peak events |
| 87 | Predictive scaling and demand forecasting | T2 | Peak events |
| 88 | Virtual waiting rooms and admission control | T2 | Peak events |
| 89 | **Payment gateway resilience and multi-gateway routing** | T1 | Peak events |
| 90 | Bot mitigation and fraud detection | T2 | Peak events |

**T1 count: 34.** That's your core. Everything else is depth you add if there's time.

**Group 11 is the deep-dive section** — payments, inventory, saga rollback, and distributed logging and tracing, each taken further than anything else in this document. If you are short on time, those five plus idempotency are the highest-value pages here. **Group 12 covers peak events and flash sales**, which is the archetypal Indian e-commerce interview question.

---

# Group 1 — The request path

How a tap on a phone in a small town becomes a row in your database. Interviewers often start here because it's where you show whether you understand the whole system or just your service.

## 1. DNS and how a request finds your server · T3

**What it is.** The phone book of the internet. `api.kiranaclub.com` becomes an IP address. **GeoDNS** returns a different IP depending on where you are, so an Indian user gets an Indian server. **Anycast** advertises the same IP from many locations and the network routes to the nearest.

**Example.** A retailer in Indore opens the app. DNS returns the IP of your Mumbai load balancer rather than one in Virginia, so round trips take 30ms instead of 250ms.

| Pros | Cons |
|---|---|
| Free way to route users to the nearest region | DNS changes propagate slowly because of TTL caching |
| Can be used for failover between regions | Clients and ISPs cache aggressively and ignore your TTLs |

**Interview line:** *"DNS-level routing is the cheapest geographic optimisation, but I wouldn't rely on it for fast failover because TTL caching means some clients keep hitting a dead region for minutes."*

## 2. Load balancers · T1

**What it is.** A thing that sits in front of your servers and spreads requests across them. The reason you can run ten copies of your API and have it look like one.

**L4 versus L7 — know this distinction.**

- **Layer 4** works at the TCP level. It sees IPs and ports, not the contents. Extremely fast, very dumb.
- **Layer 7** works at the HTTP level. It can read the URL path, headers and cookies, so it can route `/api/orders` to one service and `/api/catalog` to another, terminate TLS, and retry a failed request.

**Example.** Your API runs in 8 containers. An L7 load balancer (ALB, Nginx) receives `POST /orders`, picks a healthy container, forwards it, and if that container is dead, removes it from rotation and tries another.

**Algorithms:** round robin (simple, assumes requests cost the same), least connections (better when request cost varies — good for commerce, where a catalog query and an order placement are very different), weighted (send more to bigger machines), and hash-based (same user always lands on the same server).

**Health checks** are the part people forget. The load balancer pings each instance; failures get removed from the pool. Without them, a crashed instance keeps receiving a share of traffic and a fraction of users see errors.

| Pros | Cons |
|---|---|
| Horizontal scaling becomes possible at all | Another component that can fail — needs redundancy itself |
| Dead instances get removed automatically | L7 adds a little latency for the parsing it does |
| Zero-downtime deploys become possible | Sticky sessions undermine even distribution |
| Can terminate TLS in one place | Can become a bottleneck at very high throughput |

**Sticky sessions** pin a user to one server. Avoid them where you can — they break even load distribution and make deploys disruptive. The right fix is making services stateless so any instance works.

**Interview line:** *"L7 at the edge so I can route by path and terminate TLS, with least-connections rather than round robin because request cost varies a lot between catalog reads and order writes. Health checks with readiness probes so a starting instance doesn't get traffic before it's ready."*

## 3. Reverse proxy · T2

**What it is.** A server that sits in front of your application and forwards requests to it. Nginx is the usual one. A load balancer is a kind of reverse proxy; a reverse proxy does more than balancing.

**What it does for you:** TLS termination, gzip/brotli compression, serving static files without touching your app, request buffering (so a slow mobile upload occupies Nginx rather than your Node process), basic rate limiting, and header manipulation.

**Why request buffering matters specifically here:** your users are on slow connections. Without buffering, a retailer uploading a photo over 2G holds an application worker for 30 seconds. Nginx absorbs that instead.

| Pros | Cons |
|---|---|
| Takes slow-client handling off your app | One more hop and one more thing to configure |
| Compression and static serving for free | Misconfigured timeouts cause confusing bugs |
| One place for TLS | Can hide the real client IP if headers aren't set right |

**Interview line:** *"Nginx in front mainly for request buffering and compression — with users on slow mobile connections I don't want a slow upload occupying an application worker."*

## 4. API gateway · T1

**What it is.** One entry point for all clients that handles the concerns every service would otherwise reimplement: authentication, rate limiting, routing, request/response logging, API versioning.

**Example.** The app calls `api.kiranaclub.com` for everything. The gateway validates the JWT once, adds the retailer ID and tenant ID as trusted internal headers, applies the rate limit, and forwards to the catalog service or order service. Those services then trust the identity and don't each re-validate tokens.

| Pros | Cons |
|---|---|
| Cross-cutting concerns live in one place | Single point of failure — needs to be redundant |
| Services get simpler | Can become a bottleneck or a dumping ground for logic |
| One place to change auth or rate limits | Adds a hop of latency |
| Clients have one URL and one contract | Team coordination overhead if everyone edits it |

**The anti-pattern to name:** putting business logic in the gateway. It should route and enforce policy, not decide prices. Gateways that accumulate logic become a god service nobody can deploy safely.

**Interview line:** *"A gateway for auth, rate limiting and routing, so services don't each reimplement them. The discipline is keeping business logic out of it — the moment pricing rules live in the gateway, you've created a deployment bottleneck."*

## 5. Backend-for-Frontend (BFF) · T2

**What it is.** A thin service per client type that aggregates and shapes data for that specific client. The mobile app gets a BFF that returns exactly what its screens need, in one call.

**Why it matters enormously for this product.** A retailer on 3G pays for every round trip. If the home screen needs catalog, cart, credit balance and order status, that's four calls, each with mobile-network latency. A BFF makes it **one call returning one trimmed payload**.

**Example.** `GET /bff/home` returns `{recent_orders: [...3 items], credit_available: 24500, suggested_reorder: [...], unread_notifications: 2}` — assembled server-side from four services, trimmed to exactly what renders.

| Pros | Cons |
|---|---|
| Fewer round trips — the biggest win on slow networks | Another service to build and deploy |
| Payload shaped exactly per client, nothing wasted | Can duplicate logic across BFFs |
| Clients and services evolve independently | Risk of becoming a monolith by accident |
| Old app versions can be served by old BFF endpoints | Aggregation means one slow downstream slows the screen |

**The failure mode to name:** if the BFF calls four services serially, latency is the sum. Call them in parallel with a per-call timeout, and return partial data with the slow section degraded rather than failing the whole screen.

**Interview line:** *"For a bandwidth-constrained user base I'd put a BFF in front, because fewer round trips beats faster round trips on a mobile network. It fans out to services in parallel with per-call timeouts and degrades sections independently rather than failing the whole screen."*

## 6. CDN and edge caching · T1

**What it is.** A network of servers around the world that cache your static content close to users. The request never reaches your infrastructure.

**Example.** 50,000 product images. A retailer in a small town fetches the Parle-G image from a nearby edge node in 20ms instead of 200ms from Mumbai, and your servers never see the request.

**What to cache at the edge:** images, CSS, JS, fonts, and — often overlooked — **cacheable API responses**. A catalog listing that's the same for everyone in a region can have a short `Cache-Control` and be served from the edge, which is a huge offload.

**Invalidation:** CDN purges are slow and unreliable. **Use versioned URLs instead** — `image-v2.jpg` or a content hash. A new URL is a guaranteed cache miss; a purge is a request.

| Pros | Cons |
|---|---|
| Massive offload — static traffic never hits you | Costs money per GB served |
| Much lower latency for distant users | Invalidation is awkward; version instead |
| Absorbs traffic spikes for free | Only helps cacheable content |
| Usually includes DDoS absorption | Stale content if cache headers are wrong |

**Specific to this user base:** generate multiple image sizes on upload and serve the smallest the screen needs. A 2 MB photo on a metered connection is a real cost to a shop owner. **Say that — it's product sense, not just performance.**

**Interview line:** *"Images in object storage behind a CDN, referenced by content-hashed URLs so I never need to purge. And I'd generate thumbnails on upload, because sending a full-resolution photo to a phone displaying it at 100 pixels wide is spending the retailer's data allowance for nothing."*

## 7. TLS termination · T3

**What it is.** Decrypting HTTPS at the edge so internal services can speak plain HTTP (or their own mTLS).

**Why it's a design point:** TLS handshakes cost CPU. Doing it once at the load balancer rather than in every service saves real money, and it puts certificate management in one place.

**Interview line:** *"TLS terminates at the load balancer, with mTLS internally if we need service-to-service authentication."*

---

# Group 2 — How services talk to each other

## 8. REST API design · T1

**What it is.** Resources as nouns, HTTP verbs as actions, meaningful status codes.

**The status codes that matter in commerce:** `201` with a `Location` header on creation. `400` for malformed input versus `422` for input that parses but is semantically wrong. `409` for a conflict — a duplicate idempotency key still in flight. `429` with `Retry-After` for rate limits. `503` for overload.

**The idempotency point, which is the one they care about:** GET, PUT and DELETE are idempotent by specification. **POST is not.** That's exactly why a POST that creates an order needs an explicit `Idempotency-Key` header. Framing your Kazam work in these terms makes it instantly legible.

**Pagination:** cursor-based, never `OFFSET`, for anything that grows. Offset has to scan and discard rows, so deep pages are slow, and rows shifting between requests cause duplicates and skips.

**Versioning:** stay additive and backward-compatible as long as possible — new optional fields, never repurposing an existing one. Reach for `/v2` only on a genuine break, and run both in parallel during migration.

**Errors:** a stable machine-readable code plus a human-readable message. Clients need something to branch on that isn't prose.

**Interview line:** *"Additive versioning as the default, because with old app versions in the field for months — common with this user base, who don't update often — I can't assume everyone upgraded. Breaking changes mean running two versions in parallel."*

That last point is genuinely important here and most candidates miss it: **low-end-phone users update apps rarely, so your API has to support old clients for a long time.**

## 9. gRPC and Protobuf · T2

**What it is.** A way for services to call each other using generated code and a binary format, over HTTP/2.

**Why it's faster:** binary encoding is smaller than JSON, HTTP/2 multiplexes many calls over one connection, and the schema means no parsing ambiguity.

**Example.** Your order service calls the pricing service 50 times a second. Over gRPC that's a persistent connection with small binary messages instead of 50 TCP handshakes and JSON parsing.

| Pros | Cons |
|---|---|
| Faster and smaller than JSON over HTTP/1.1 | Not human-readable — harder to debug |
| Generated clients mean no hand-written HTTP code | Browser support needs a proxy layer |
| Strict schema catches mismatches at compile time | Another toolchain to learn and maintain |
| Streaming built in | Overkill between two services that talk rarely |

**When to use:** internal service-to-service, high call volume, teams that want a strict contract. **When not to:** public APIs (REST is universal and debuggable), or between services that exchange a handful of calls a minute.

**Interview line:** *"gRPC internally where call volume justifies it, REST at the public edge for ubiquity and debuggability. I wouldn't introduce it for two services exchanging ten calls a minute — the contract benefit doesn't cover the tooling cost."*

## 10. GraphQL · T3

**What it is.** The client sends a query describing exactly the fields it wants, and gets back exactly that.

| Pros | Cons |
|---|---|
| No over-fetching — good for slow networks | Caching is much harder than with REST |
| One round trip for data from several sources | A client can write a query that destroys your database |
| Frontend iterates without backend changes | N+1 query problems are easy to create |
| Self-documenting schema | Real operational complexity |

**The honest position:** a BFF gets you most of GraphQL's benefit for a single known client, without the complexity. GraphQL earns its keep when you have many different clients with genuinely different data needs.

**Interview line:** *"For one mobile client, I'd use a BFF rather than GraphQL — same benefit of trimmed payloads and one round trip, far less operational surface. GraphQL pays off with many diverse clients."*

## 11. WebSockets vs SSE vs polling · T2

**The four options for getting server updates to a client:**

- **Short polling** — client asks every N seconds. Simple, wasteful, delayed.
- **Long polling** — client asks, server holds the request open until something happens. Lower latency, holds connections.
- **Server-Sent Events (SSE)** — one long-lived HTTP connection, server pushes. One-directional, auto-reconnects, works through most proxies.
- **WebSockets** — full duplex, both sides push. Most powerful, most expensive.

| | Pros | Cons |
|---|---|---|
| **Polling** | Trivially simple, stateless, works everywhere | Wasted requests, delayed updates |
| **Long polling** | Near-real-time, standard HTTP | Holds server connections open |
| **SSE** | Simple, auto-reconnect, cheap | Server-to-client only |
| **WebSockets** | Bidirectional and real-time | Stateful — breaks horizontal scaling without Redis pub-sub; reconnects constantly on flaky networks; burns battery |

**The judgement call for this product, and it's a good one to state:** *"For order status updates to retailers on patchy mobile networks, I'd use polling at a sensible interval rather than WebSockets. A socket on a flaky connection reconnects constantly, which burns the user's battery and data and churns server connections for no benefit. Real-time isn't a requirement here — knowing within 30 seconds is fine."*

**If you do use WebSockets:** connections are pinned to one process, so you need Redis pub-sub to route a message to whichever instance holds that user's socket, plus heartbeats, reconnection with backoff, and a decision about whether missed messages are replayed or dropped.

## 12. Webhooks · T1

**What it is.** The reverse of an API call — a third party calls *you* when something happens. Payment gateways, distributor systems and logistics partners all work this way.

**The full checklist, and you've built this:**

- **Verify the signature.** HMAC over the raw body with a shared secret, constant-time comparison. Without this, anyone can POST you a fake "payment succeeded."
- **Include a timestamp in the signed data** with a tolerance window, so an old captured request can't be replayed.
- **Deduplicate on the provider's event ID.** They will send duplicates.
- **Expect out-of-order delivery.** "Delivered" can arrive before "dispatched." Use sequence numbers or source timestamps, plus a state machine that rejects illegal backwards transitions.
- **Respond fast — acknowledge, then process asynchronously.** Doing real work inside the handler means the sender times out and retries, multiplying your load exactly when you're slow.
- **Be idempotent.** Same event twice must have the same effect as once.

| Pros | Cons |
|---|---|
| No polling — you hear about events immediately | You don't control delivery reliability |
| Scales better than everyone polling you | Duplicates and out-of-order are normal |
| Standard across payment and logistics providers | Needs signature verification or it's a security hole |
| | Your endpoint must be publicly reachable and always up |

**Interview line:** *"This is what I built at Kazam — signature verification, dedup on the provider's event ID, acknowledge immediately and process async, and a state machine that rejects a late webhook trying to move a completed order backwards."*

## 13. Serialization and schema evolution · T2

**What it is.** How data is encoded on the wire, and how you change that format without breaking everyone.

**JSON** is readable and universal, but verbose and untyped. **Protobuf** and **Avro** are compact and schema-driven.

**The part that actually matters: schema evolution.** When a producer adds a field and consumers haven't been updated, what happens? The rules: **add optional fields, never remove or repurpose existing ones, never change a field's type, and never reuse a field number** in Protobuf. A **schema registry** enforces these automatically.

**Why it matters here:** you'll have old mobile app versions in the field for months, plus distributor integrations you can't force to upgrade. **Backward compatibility isn't a nicety, it's a constraint.**

**Interview line:** *"Schema changes stay additive, because I can't force old app versions or partner integrations to upgrade on my schedule. Removing a field is a multi-release process, not an edit."*

## 14. Service discovery · T3

**What it is.** How a service finds the current addresses of another service, when containers are constantly being created and destroyed.

**Options:** DNS-based (simple, TTL-limited), a registry like Consul (services register themselves), or the platform's own mechanism in Kubernetes or ECS (usually the right answer — don't build this).

**Interview line:** *"I'd use whatever the platform provides — ECS service discovery or Kubernetes services. Building your own registry is solving a solved problem."*

## 15. Service mesh · T3

**What it is.** A sidecar proxy next to every service that handles retries, mTLS, circuit breaking, and telemetry, so application code doesn't.

| Pros | Cons |
|---|---|
| Resilience and observability without touching app code | Significant operational complexity |
| Consistent policy across languages | Another layer when debugging |
| mTLS everywhere for free | Resource overhead per pod |

**Interview line:** *"A mesh is usually premature. At a handful of services I'd put retries and circuit breaking in a shared library, and consider a mesh when we have enough services in enough languages that a library stops being practical."*

---

# Group 3 — Storage

The group that matters most for a commerce platform, and your strongest ground.

## 16. Storage engines: B-tree vs LSM-tree · T2

**What it is.** How a database physically writes data to disk. There are two families and knowing the difference explains why Postgres and Cassandra behave so differently.

**B-tree** (Postgres, MySQL) keeps data in a sorted tree and **updates pages in place**. Reads are fast and predictable — a few page lookups to find any row. Writes are slower because you may have to rewrite a page and update several indexes.

**LSM-tree** (Cassandra, RocksDB, ScyllaDB) **never updates in place**. Writes go to an in-memory table and an append-only log, and periodically get flushed and merged into sorted files on disk. Writes are extremely fast because they're sequential appends. Reads are slower because a key might live in several files, so you check each one — which is where Bloom filters come in.

**Example.** Writing 10,000 order rows per second: an LSM engine appends them sequentially, very fast. Reading one specific order by ID: a B-tree finds it in three page reads; an LSM engine may check five files first.

| | Pros | Cons |
|---|---|---|
| **B-tree** | Fast, predictable reads. Mature. Supports transactions and constraints well. | Slower writes. Write amplification from page rewrites. |
| **LSM-tree** | Very fast writes. Good compression. | Slower and less predictable reads. Compaction consumes I/O in bursts. |

**Interview line:** *"Commerce is read-heavy and correctness-critical, so a B-tree engine like Postgres is the right default. I'd consider an LSM store for something genuinely write-heavy and simple-to-read, like an event or audit log — but not for orders, where I want constraints and transactions."*

## 17. Write-ahead log (WAL) · T2

**What it is.** Before changing any data page, the database writes the change to an append-only log and flushes that to disk. If the server loses power mid-write, recovery replays the log.

**Why it's worth knowing** — three things in your system depend on it:

1. **Durability.** The "D" in ACID is the WAL.
2. **Replication.** Replicas are fed by streaming the primary's WAL.
3. **Change data capture.** Tools like Debezium read the WAL to turn database changes into events.

**The operational gotcha to name:** if a replica falls behind or a replication slot is inactive, the primary **keeps WAL files it can't delete** and the disk fills up. An inactive replication slot filling a production disk is a genuine, common incident.

**Interview line:** *"The WAL is what gives you durability, replication and CDC from the same mechanism. The thing to monitor is replication slot lag, because an abandoned slot will fill the primary's disk."*

## 18. Indexing · T1

**What it is.** A sorted structure so the database doesn't read every row.

**Types and when each applies:**

- **B-tree** — the default. Equality, ranges, sorting, prefix matching.
- **GIN** — inverted index for values containing many searchable pieces: `jsonb`, arrays, full-text search. Slower writes, bigger.
- **GiST** — the framework for geometric data, ranges, nearest-neighbour. **What PostGIS uses.** You used this on Pujo Atlas.
- **BRIN** — tiny; good for huge tables where physical order correlates with the value, like an append-only events table on `created_at`.
- **Hash** — rarely worth it.

**The rules that come up:**

**Leftmost prefix.** An index on `(retailer_id, status, created_at)` serves a filter on `retailer_id`, or `retailer_id + status`, or all three — **not `status` alone**. Column order is a design decision.

**Partial indexes.** `WHERE status = 'pending'` makes a tiny index when 99% of rows are `completed`. Ideal for a work queue.

**Covering indexes.** `INCLUDE (...)` lets the query be answered entirely from the index without touching the table.

**Why an index silently isn't used:** the filter wraps the column in a function (needs an expression index), a type mismatch forces a cast, low selectivity makes a sequential scan genuinely cheaper, statistics are stale, or `LIKE '%x'` has a leading wildcard.

| Pros | Cons |
|---|---|
| Often a 1000x read speedup | Slows every write — every insert updates every index |
| Cheap and reversible | Consumes disk and memory |
| No application changes | An unused index is pure cost nobody notices |

**Interview line:** *"Before I reach for a cache I check the index, because a missing index is usually the actual problem and it costs nothing in consistency. A cache is a second source of truth that can lie."*

## 19. Replication · T1

**What it is.** Keeping copies of your data on other machines.

**Leader-follower (the common model).** Writes go to the leader. The leader streams its WAL to followers. Reads can go to either.

**Synchronous vs asynchronous.** Synchronous means the leader waits for a follower to confirm before acknowledging your write — no data loss on failover, but a slow follower stalls all writes. Asynchronous is fast but means **replication lag**, and a failover can lose recently acknowledged writes.

**Multi-leader.** Writes accepted in several places. Needed for multi-region writes, but you now have **write conflicts** to resolve, which is genuinely hard. Avoid unless you must.

**Leaderless (Dynamo-style).** Write to several nodes, read from several, use quorums. **If R + W > N**, any read overlaps at least one node with the latest write, giving strong consistency. Tunable, but you're now doing conflict resolution in application code.

| Pros                                     | Cons                                   |
| ---------------------------------------- | -------------------------------------- |
| Scales reads nearly linearly and cheaply | Lag causes stale reads                 |
| Gives you a failover target              | Doesn't help write throughput at all   |
| Analytics can run off a replica          | More infrastructure to run and monitor |

**The bug you must be able to name — read-your-writes.** Retailer places an order, the write goes to the leader, the app immediately loads "My Orders," that read hits a lagging replica, **and the order isn't there.** The retailer panics and orders again. Fixes: route that user's reads to the leader for a few seconds after their write, pin the session briefly, or return the created object in the write response so no re-read is needed.

**Interview line:** *"Read replicas are the first read-scaling lever because they're cheap and need no rewrite. The thing I'd handle carefully is read-your-writes — a retailer who just placed an order has to see it, so that specific read goes to the primary for a short window."*

## 20. Partitioning and sharding · T1

**Two different things people confuse.**

**Partitioning** splits one table into pieces **inside one database**. Postgres does it natively. `orders` becomes `orders_2026_01`, `orders_2026_02`. You keep joins, transactions and constraints.

**Sharding** splits data across **separate databases**. You lose cross-shard joins and transactions.

**Partitioning strategies:** by **range** (date is the classic — queries for last month touch one partition, and archiving last year is an instant `DETACH` instead of a giant `DELETE`); by **list** (region); by **hash** (even spread, but you lose range pruning).

**Sharding strategies:** range, hash, **consistent hashing** (see next topic), or a **directory** — a lookup table mapping each key to a shard, which is flexible and lets you move a tenant, at the cost of a lookup and a new critical component.

**Choosing a shard key.** It must be something nearly every query filters on. In B2B commerce that's `retailer_id` or `tenant_id`. **If you shard orders by `order_id`, then "show me this retailer's orders" has to hit every shard** — you've made the most common query the most expensive one.

**The hot shard problem.** If one distributor does 30% of volume and you shard by distributor, one shard melts while the rest idle. Fix by salting the key or giving that tenant dedicated capacity.

| | Pros | Cons |
|---|---|---|
| **Partitioning** | Smaller indexes, faster scans, instant archival, keeps joins and transactions | Needs a good partition key; queries without it hit every partition |
| **Sharding** | No ceiling on writes or storage; failure isolated to one shard | No cross-shard joins or transactions; every query needs the key; rebalancing is brutal; hot shards are common |

**Interview line, and it's one of your strongest:** *"At around 80,000 orders a day, sharding is premature — one Postgres primary handles that for years. I'd partition orders by month for query performance and cheap archival. The trigger to actually shard would be write rate approaching what one primary can take, or the dataset outgrowing one machine's disk. I'd want to see that number first, because sharding is a one-way door."*

## 21. Consistent hashing · T2

**What it is.** A way to assign keys to servers so that adding or removing a server moves as little data as possible.

**The problem it solves.** The naive approach is `server = hash(key) % N`. Add one server and N changes, so **almost every key now maps somewhere different** — your entire cache is invalidated at once, and every request misses and hits the database. That's an outage.

**How it works.** Imagine servers and keys both placed on a circle. Each key belongs to the next server clockwise. Add a server and only the keys between it and its predecessor move — roughly 1/N of the data instead of all of it. **Virtual nodes** (each physical server appearing at many points on the circle) smooth out the distribution.

**Example.** Your Redis cluster has 4 nodes. You add a fifth. With modulo hashing, ~80% of keys relocate and your database gets hammered. With consistent hashing, ~20% relocate.

| Pros | Cons |
|---|---|
| Adding or removing a node moves minimal data | More complex than modulo |
| No mass cache invalidation on a topology change | Uneven distribution without virtual nodes |
| Used by Redis Cluster, Cassandra, DynamoDB, CDNs | Doesn't solve hot keys — one popular key is still one node |

**Interview line:** *"Consistent hashing so adding a cache node doesn't invalidate everything at once. It doesn't solve hot keys though — a single popular key still lands on one node, and for that you need local caching in front or key splitting."*

## 22. Federation (functional partitioning) · T3

**What it is.** Splitting databases by function rather than by rows. Orders in one database, catalog in another, analytics in a third.

**Pros:** each can be sized and tuned for its own workload; smaller individual datasets. **Cons:** you lose joins across them, and you've introduced the same cross-boundary consistency problems as microservices.

**Interview line:** *"Functional splits are usually a better first move than row-level sharding, because the boundaries follow the domain and a lot of queries never crossed them anyway."*

## 23. Materialised views · T2

**What it is.** A query whose results are physically stored, so reading it is a table scan of pre-computed rows rather than re-running an expensive aggregation.

**Example.** "Total GMV per distributor per day" over a year of orders is an expensive `GROUP BY`. As a materialised view refreshed nightly, it's a cheap lookup.

**The refresh question is the whole trade-off.** Full refresh is simple but expensive and locks (unless you use `REFRESH ... CONCURRENTLY`). Incremental refresh is cheap but you have to build it. Event-driven update is freshest but most work.

| Pros | Cons |
|---|---|
| Turns expensive aggregations into cheap lookups | Stale between refreshes |
| Built into Postgres — no new infrastructure | Refresh can be expensive and needs scheduling |
| Easy to explain and reason about | Doesn't help real-time needs |

**Interview line:** *"Materialised views for dashboards and reporting aggregates, refreshed on a schedule the business agrees to. They're the cheapest form of a read model — no new infrastructure, just a refresh job."*

## 24. Object storage · T2

**What it is.** S3 and equivalents. Cheap, effectively infinite, highly durable storage for files. Not a filesystem and not a database — you get and put whole objects by key.

**The rules:**

- **Never store files in your database.** Blobs bloat the table, slow backups, and consume the buffer cache that your real queries need.
- **Upload directly from the client with a presigned URL.** The client asks your API for a short-lived signed URL, then uploads straight to S3. The file never passes through your API, so a slow 2G upload doesn't occupy an application worker.
- **Serve through a CDN**, not from your app.
- **Use lifecycle rules** to move old files to colder, cheaper storage automatically.

| Pros                                          | Cons                                                 |
| --------------------------------------------- | ---------------------------------------------------- |
| Extremely cheap and durable                   | Higher latency than local disk                       |
| Scales without you thinking about it          | Eventual consistency on some operations historically |
| Lifecycle rules handle archival automatically | Egress costs money — a CDN in front matters          |

**Interview line:** *"Images and documents go to S3 with presigned-URL uploads straight from the client, so a slow mobile upload never occupies an app server, and served through a CDN so egress is cheap."*

## 25. Tiered storage and archival · T3

**What it is.** Moving old data to cheaper storage. Hot data in Postgres, warm in cheaper storage, cold in S3 Glacier.

**Why it matters in commerce:** you keep order history for years for legal and accounting reasons, but 99% of queries touch the last 90 days. Keeping seven years of orders in your hot database makes every index bigger and every backup slower for no benefit.

**With partitioned tables this is easy:** detach the old partition and archive it. Without partitioning, it's a painful mass delete that bloats the table.

**Interview line:** *"Partitioning by month gives me archival almost for free — detach the old partition and move it to cold storage, rather than a mass delete that bloats the table and leaves vacuum to clean up."*

## 26. Columnar and time-series stores · T2

**What it is.** Row stores (Postgres) keep a whole row together, which is right when you read whole rows. **Columnar** stores (ClickHouse, BigQuery, Redshift) keep each column together, which is right when you scan one column across millions of rows.

**Example.** "Sum of order value by category for the last year." A row store reads every full order row. A columnar store reads only the two columns it needs and compresses them well — often 10–100x faster for this shape.

| Pros | Cons |
|---|---|
| Enormously faster analytical scans | Terrible at single-row lookups and updates |
| Excellent compression | Usually batch-loaded, so data is minutes behind |
| Scales to billions of rows cheaply | A separate system to run |

**The judgement line:** *"At this volume, reporting off a read replica is enough and costs nothing extra. I'd move to a columnar store when analytical queries start taking minutes, or when the business wants to join order data with sources outside the platform."*

## 27. Data warehouse, ETL and ELT · T3

**What it is.** A central store for analytics, fed from your operational databases. **ETL** transforms before loading; **ELT** loads raw then transforms inside the warehouse, which is the modern default because storage is cheap and it keeps the raw data for re-processing.

**Why it matters in an interview:** separating the operational database from the analytical one is a basic maturity signal. An outage caused by someone's dashboard query is a bad day.

**Interview line:** *"Operational and analytical workloads get separated early, even if it's just a read replica at first, because one unbounded GROUP BY against the primary can take down order placement."*

## 28. Change data capture (CDC) · T2

**What it is.** Reading the database's write-ahead log to turn every insert, update and delete into an event stream. Debezium is the usual tool.

**Why it's powerful.** Your application doesn't have to publish events at all — the database changes *are* the events. Nothing can be missed, because nothing gets into the database without passing through the WAL.

**Example.** A price change in Postgres automatically produces an event that updates the Elasticsearch index, invalidates the cache, and feeds the warehouse — with no application code publishing anything.

| Pros                                                | Cons                                                       |
| --------------------------------------------------- | ---------------------------------------------------------- |
| Cannot miss a change — it's the WAL                 | Events are database-shaped, not business-shaped            |
| No application changes needed                       | Couples consumers to your schema                           |
| Great for keeping search indexes and caches in sync | Operationally heavy (connectors, offsets, schema handling) |

**CDC versus the transactional outbox — know the difference, it's a good interview moment.** CDC gives you *"the `orders` row changed."* The outbox gives you *"an `OrderPlaced` event happened, with these business fields."* The outbox produces a clean domain event you control; CDC leaks your schema to consumers. **For domain events, outbox. For syncing derived stores like a search index, CDC is excellent.**

**Interview line:** *"I'd use the outbox for domain events, because I want to publish a business fact I control rather than a row shape that couples consumers to my schema. CDC I'd use for keeping derived stores like Elasticsearch in sync, where the row shape is exactly what I want."*

---

# Group 4 — Caching

## 29. Multi-level caching · T1

**What it is.** Caching happens at several layers, and knowing all of them lets you push work as far from your database as possible.

| Layer                         | What it holds                                                                      | Lifetime                            |
| ----------------------------- | ---------------------------------------------------------------------------------- | ----------------------------------- |
| **Client / app**              | Catalog data, images, last order                                                   | Until invalidated by the app        |
| **CDN / edge**                | Images, static assets, cacheable API responses                                     | Minutes to forever (versioned URLs) |
| **API gateway**               | Identical GET responses                                                            | Seconds                             |
| **Application memory**        | Very hot, small, rarely-changing data — feature flags, config, segment definitions | Seconds to minutes                  |
| **Distributed cache (Redis)** | Sessions, resolved price lists, read models, rate-limit counters                   | Minutes to hours                    |
| **Database buffer cache**     | Recently read pages                                                                | Managed by Postgres                 |

**The principle: the cheapest request is the one that never reaches you.** Each layer up the chain is an order of magnitude cheaper.

**Example for this product.** A retailer opens the catalog. Images come from the CDN (never reaches you). The category list comes from in-process memory (never reaches Redis). The resolved price list for their segment comes from Redis (never reaches Postgres). Only their personalised reorder suggestions touch the database.

**The in-process caching caveat worth naming:** each instance has its own copy, so they go stale independently and you can't invalidate them reliably. Use it only for small, slow-changing data where a few seconds of inconsistency between instances is harmless.

**Interview line:** *"I think about caching in layers, pushing as far toward the client as the correctness requirement allows. Images at the CDN, segment price lists in Redis, and only genuinely personalised data hitting Postgres."*

## 30. Cache patterns and invalidation · T1

**The patterns:**

- **Cache-aside** — app checks cache, misses, reads the database, writes it to the cache. The default.
- **Read-through** — the cache layer does the database read itself.
- **Write-through** — write to cache and database together. Consistent, slower writes.
- **Write-behind** — write to cache, flush to the database later. Fastest, can lose data.

**Invalidation is the hard part and you should say so.**

| Strategy                      | Pros                                      | Cons                                 |
| ----------------------------- | ----------------------------------------- | ------------------------------------ |
| **TTL only**                  | Dead simple, self-healing                 | Stale for up to the TTL              |
| **Delete on write**           | Much fresher                              | Has a resurrection race (below)      |
| **Versioned keys**            | No race at all; new write makes a new key | Uses more memory; old keys linger    |
| **Event-driven invalidation** | Precise                                   | Most machinery; events can be missed |

**The resurrection race — name this unprompted, it's a strong signal.** A reader misses the cache and reads the database. Before it writes that value into the cache, a writer updates the database and deletes the cache key. Then the reader writes its *old* value into the cache. **The stale value is now cached indefinitely.** Mitigations: always set a TTL as a backstop even when you delete on write, delete again after a short delay, or use versioned keys so the problem can't occur.

**What NOT to cache:** inventory counts and credit limits. Cache "47 available" and serve it to a hundred users and you oversell. **Approximate for display is fine; the number checked at commitment comes from the source of truth inside the transaction.** That distinction is a real technical-depth signal.

**Interview line:** *"Caching is easy, invalidation is the hard part. I'd start with a TTL I can justify from how often the data actually changes, and build event-driven invalidation only where staleness is genuinely unacceptable. And I'd never cache stock at the point of commitment."*

## 31. Eviction policies · T2

**What it is.** What the cache throws away when memory fills.

- **LRU** — least recently used. The sensible default for most caches.
- **LFU** — least frequently used. Better when there's a stable set of hot keys and occasional one-off scans that would pollute an LRU.
- **TTL-based** — evict expired first.
- **`noeviction`** — reject writes when full. Use this when Redis holds data you cannot lose.

**The architecture question worth asking out loud:** *"is this Redis a cache or a source of truth?"* If losing it entirely is survivable, it's a cache, use `allkeys-lru`, and design for cold start. If it isn't survivable, you need persistence and replication — and you should ask whether that data belongs in a database instead.

**The cold-start problem to name:** after a deploy or a flush, every request misses at once and your database takes the full load. Mitigations: pre-warm the cache before shifting traffic, or ramp traffic gradually.

## 32. Bloom filters · T3

**What it is.** A tiny memory structure that answers "have I definitely never seen this?" It can say **"definitely not present"** or **"possibly present"** — never a false negative, sometimes a false positive.

**Example.** Before hitting the database to check whether a barcode exists in your catalog, check a Bloom filter holding all known barcodes. If it says no, you skip the query entirely. A few megabytes can cover millions of keys.

**Where it's actually used:** LSM-tree databases use them to avoid reading files that can't contain a key. Also useful for "has this user already seen this post" in a feed, and for cheap duplicate detection.

| Pros | Cons |
|---|---|
| Extremely small memory footprint | False positives (tunable, never false negatives) |
| Very fast | Can't delete from a standard Bloom filter |
| Avoids expensive lookups for things that don't exist | Only answers membership, not retrieval |

**Interview line:** *"A Bloom filter in front of an expensive lookup when most queries are for things that don't exist — it eliminates those at almost no memory cost."*

## 33. Cache stampede · T1

**What it is.** A hot key expires. A thousand concurrent requests all miss simultaneously, all hit the database at once, and the database falls over — at exactly the moment the key was most popular.

**Example.** The homepage catalog for a region, cached with a 5-minute TTL. At the 5-minute mark, every request in that region misses together.

**The fixes:**

- **Jittered TTLs** — add randomness so keys don't expire in lockstep. The cheapest fix and it should be the default.
- **Single-flight lock** — the first request to miss takes a lock and recomputes; the rest wait briefly and read the new value.
- **Probabilistic early recomputation** — refresh *before* expiry with a probability that rises as expiry approaches, so one request refreshes while others are still being served the cached value.
- **Stale-while-revalidate** — serve the stale value and refresh in the background. Best user experience; requires accepting staleness.

**The related failure — cold start.** Same shape, different trigger: a deploy or cache flush empties everything at once. Pre-warm before shifting traffic.

**Interview line:** *"Jittered TTLs as the default so keys don't expire together, and single-flight on genuinely hot keys so only one request recomputes. Before a flash sale I'd pre-warm the cache, because the worst time to have a cold cache is the moment traffic peaks."*

---

# Group 5 — Async and data flow

## 34. Message queues · T1

**What it is.** A buffer between a producer and a consumer. The producer drops work in and moves on; a consumer picks it up when it can.

**Example.** Order placed. Instead of sending the SMS inline (adding a second to the response and letting an SMS failure fail the order), you push a job onto a queue. A worker sends it. If the SMS provider is down, the job retries later and the order is unaffected.

**What a queue gives you beyond "later":**

- **Shock absorption.** A traffic spike fills the queue instead of overwhelming workers. The queue depth becomes your early warning.
- **Retries with backoff**, built in.
- **Failure isolation.** The SMS provider being down doesn't touch order placement.
- **Independent scaling.** Add workers without touching the API.

| Pros                                             | Cons                                                  |
| ------------------------------------------------ | ----------------------------------------------------- |
| Fast responses; users only wait for what matters | Eventual consistency — "soon," not "now"              |
| Side-effect failures can't fail the main action  | Much harder to debug; no single stack trace           |
| Absorbs bursts                                   | Consumers must be idempotent (at-least-once delivery) |
| Independent scaling                              | More infrastructure                                   |

**The judgement point most people miss:** you don't need Kafka or RabbitMQ to have a queue. **A Postgres table with `SELECT ... FOR UPDATE SKIP LOCKED`** is a perfectly good job queue — it skips rows another worker has locked, so N workers pull different jobs with no coordination. Zero new infrastructure, transactional with your other writes, and trivially debuggable with SQL.

**Interview line:** *"At one order per second I'd use a Postgres-backed queue with `FOR UPDATE SKIP LOCKED` before adding a broker. It's transactional with the rest of my writes, I can debug it with SQL, and it's zero new infrastructure. I'd move to a real broker when throughput or multiple independent consumers justify it."*

## 35. Event streaming (the log) · T1

**What it is.** An append-only log of facts, split into partitions, that many independent consumers can read at their own pace and replay from the beginning.

**How it differs from a queue, which is the thing to get right:** in a queue, a message is consumed and gone — it's *work* for one consumer. In a log, the message stays, and many consumer groups each track their own position — it's a *fact* that many parties care about.

**Example.** `OrderPlaced` is a fact. The notification service, the analytics pipeline, the distributor integration, and the loyalty service all care, independently. With a queue you'd need four queues and a fan-out. With a log they each read the same stream at their own pace, and a new fifth consumer can replay history from the start.

**The three things to know about Kafka specifically:**

1. **Ordering is guaranteed only within a partition**, never across a topic. So if all events for one order must be processed in order, **key by order ID** so they land in the same partition. Key by something with few distinct values and you create hot partitions; key by something too fine-grained and you lose the ordering you wanted.
2. **Consumer groups** give parallelism: each partition is read by exactly one consumer in the group, so **max parallelism equals partition count** and extra consumers sit idle.
3. **Rebalances** pause consumption when group membership changes — which is why a consumer that takes too long between polls gets kicked out and triggers a rebalance storm. Classic production failure.

**Consumer lag** is the health metric: how far behind the end of the log you are. Rising lag means you're not keeping up.

| Pros                                             | Cons                             |
| ------------------------------------------------ | -------------------------------- |
| Many independent consumers from one stream       | Operationally heavy              |
| Replayable — new consumers can reprocess history | No per-message acknowledgement   |
| Very high throughput                             | Ordering only within a partition |
| Doubles as an audit log                          | Overkill at low volume           |
|                                                  |                                  |

**Interview line:** *"I'd bring in Kafka when several independent teams need the same event stream, or when I want replay — not for throughput. At one order per second, throughput isn't the argument."*

## 36. Pub-sub · T2

**What it is.** Publishers emit to a topic; any number of subscribers receive a copy. The publisher doesn't know who's listening.

**Fan-out vs work queue — the distinction that matters.** Pub-sub means *everyone* gets a copy. A work queue means *one* consumer gets it. Getting these backwards is a real bug: if your SMS service subscribes to a pub-sub topic and you run three instances, **all three send the SMS**. You need a consumer group (one per group) rather than plain pub-sub.

**Interview line:** *"Pub-sub for fan-out where every subscriber needs its own copy; consumer groups when I want exactly one of my instances to handle each message. Mixing those up is how you send the same SMS three times."*

## 37. Delivery semantics · T1

**The three options, and only two are real:**

- **At-most-once** — commit the offset before processing. A crash loses the message. Rarely acceptable.
- **At-least-once** — commit after processing. A crash means reprocessing. **The standard.**
- **Exactly-once** — doesn't exist across a network boundary.

**Why exactly-once is impossible, and you should be able to explain it:** a timeout is ambiguous. When your call times out you cannot tell whether the request never arrived, arrived and is still processing, or completed and the response was lost. Since you can't tell, you retry. Since you retry, duplicates happen.

**What you actually build: at-least-once delivery plus idempotent consumers, which gives you effectively-once processing.** Say that sentence confidently — candidates who claim they implemented exactly-once delivery mark themselves immediately.

**The nuance worth adding:** Kafka's transactions give exactly-once *within Kafka* for read-process-write between topics. The moment you touch anything outside — charge a card, call a distributor's API — you're back to needing idempotency on your side.

**Interview line:** *"Exactly-once delivery across a network is impossible. What I build is at-least-once plus idempotent consumers, which gives effectively-once processing. That's why idempotency isn't optional in any event-driven system."*

## 38. Transactional outbox · T1

**The problem.** You need to save the order to Postgres *and* publish `OrderPlaced`. Two different systems, no shared transaction. Commit then crash before publishing, and the order exists but nobody downstream knows — no SMS, no distributor notified. Publish first and fail the commit, and you've announced an order that doesn't exist.

**The fix.** In **one local transaction**, write the order row *and* a row into an `outbox` table. Atomic — both or neither. A separate relay process reads unsent outbox rows, publishes them, and marks them sent (use `FOR UPDATE SKIP LOCKED` so multiple relay instances don't collide).

**Why it works.** The only remaining failure is the relay crashing after publishing but before marking sent, which publishes the event twice. And duplicates are a solved problem — idempotent consumers. **You've converted an unsolvable problem into a solved one.**

| Pros                                        | Cons                                    |
| ------------------------------------------- | --------------------------------------- |
| Events can never be lost                    | Small publishing delay                  |
| No new infrastructure if you poll the table | A relay process to run and monitor      |
| Reuses a transaction you already have       | Consumers must be idempotent            |
| The outbox doubles as an audit trail        | Table needs cleanup or it grows forever |

**Interview line:** *"Transactional outbox. Order row and event row in the same transaction, a relay publishes with `FOR UPDATE SKIP LOCKED`, at-least-once so consumers dedupe on event ID. It's the standard way to make your database and your event stream agree without a distributed transaction."*

## 39. Dead letter queues · T2

**What it is.** A separate queue for messages that keep failing, so they stop blocking everything else.

**The failure it prevents — the poison pill.** One malformed message fails, retries, fails, retries, forever. If ordering matters and you retry in place, **that one message blocks its entire partition permanently.** Everything behind it stops.

**The pattern:** bounded retries with backoff, then move it to the DLQ and carry on. Then — and this is the part people forget — **alert on the DLQ.** A silently filling dead letter queue is a dropped-data incident waiting to be discovered weeks later.

**Interview line:** *"Bounded retries then a dead letter queue, with an alert on DLQ depth. An unmonitored DLQ is just a place where data goes to be forgotten."*

## 40. Batch vs stream processing · T2

**Batch** processes a large chunk on a schedule. **Stream** processes each event as it arrives.

**Example.** Daily settlement reconciliation is batch — it runs at 2am against the day's complete data, and it's simple, restartable and easy to reason about. Fraud detection on order placement is stream — a day late is useless.

| | Pros | Cons |
|---|---|---|
| **Batch** | Simple, restartable, easy to test, efficient per record | High latency; a failed run can mean a day's delay |
| **Stream** | Low latency; smooth resource usage | Harder — late data, out-of-order events, windowing, state management |

**The judgement point:** most things people want to stream can be batched on a short interval, and a 5-minute batch is dramatically simpler than a stream processor. Reach for streaming when the latency requirement genuinely demands it.

**Interview line:** *"I'd default to batch on a short interval and move to streaming only where latency genuinely matters, because stream processing brings late-arrival and windowing problems that a batch job just doesn't have."*

## 41. Lambda and Kappa architecture · T3

**Lambda** runs a batch layer (accurate, slow) and a speed layer (fast, approximate) side by side and merges them. **Kappa** says that's two codebases doing the same thing, so just use the stream and replay it when you need to recompute.

**Interview line:** *"Lambda's real problem is maintaining the same logic twice. Kappa is cleaner if your log retains enough history to replay."*

## 42. Backpressure · T2

**What it is.** A slow consumer signalling upstream to slow down, instead of silently accumulating an unbounded buffer until it runs out of memory.

**Example.** Your fulfilment worker reads orders faster than the distributor's API can accept them. Without backpressure, your in-memory buffer grows until the process dies. With it, the worker stops pulling until it has capacity.

**The general principle, which is worth stating:** **under overload, a bounded queue with load shedding degrades gracefully; an unbounded one collapses.** A request sitting in your queue that already timed out on the client's side is pure waste — you're doing work nobody will read while new work queues behind it.

**Interview line:** *"Every queue needs a bound. An unbounded queue just converts a throughput problem into an out-of-memory crash, and it does it at the worst possible moment."*

## 43. Distributed scheduling · T2

**What it is.** Running scheduled jobs when you have many instances — releasing expired inventory reservations, running daily reconciliation, sending reorder reminders.

**The bug:** you deploy a cron inside your service and run 8 instances, so the job runs 8 times. Reorder reminders go out 8 times to every retailer.

**The fixes:**

- **A Postgres advisory lock** — `pg_advisory_lock` on a job-specific integer. Whoever gets it runs. Simple, uses what you already have.
- **A `jobs` table with a claim**, using the same conditional-update pattern as inventory.
- **A platform scheduler** — ECS scheduled tasks, Kubernetes CronJob — which runs one instance by design. Usually the right answer.

**And the jobs themselves must be idempotent and restartable**, because "ran twice" and "died halfway" are both normal. Process in batches with a checkpoint, not one giant transaction over a million rows.

**Interview line:** *"Scheduled jobs go through the platform's scheduler, or take an advisory lock if they live in the service. And they're written to be idempotent and restartable in batches, because a job that can only succeed as one giant transaction will eventually fail as one giant transaction."*

---

# Group 6 — Consistency and coordination

## 44. CAP and PACELC · T1

**CAP, stated correctly.** During a network partition you must choose between consistency and availability. **The common version — "pick two of three" — is wrong.** Partitions are not a choice you make; they happen to you. The theorem is only about what you do when one occurs.

**Example.** Your database is split across two data centres and the link drops. Either the minority side refuses writes (consistent, not available) or it accepts them and you reconcile later (available, not consistent).

**PACELC is the more useful version.** During a **P**artition choose **A**vailability or **C**onsistency; **E**lse — in normal operation — choose **L**atency or **C**onsistency. **The "else" half governs daily design decisions**, because partitions are rare and the latency-vs-consistency trade is constant. Every time you read from a replica instead of the primary, you're making the PACELC "else" choice.

**Interview line:** *"CAP only describes what happens during a partition, and partitions are rare. PACELC's second half is what I actually use day to day — every read-replica decision is trading consistency for latency."*

## 45. Consistency models · T1

Weakest to strongest:

- **Eventual** — replicas converge if writes stop. Fine for a catalog description.
- **Read-your-writes** — you see your own updates. **Usually the minimum acceptable for a UI.**
- **Monotonic reads** — you never see time go backwards (an order appearing, then disappearing on refresh).
- **Causal** — operations with a cause-and-effect relationship are seen in order. A reply never appears before the post it replies to.
- **Linearizable / strong** — behaves as if there's one copy, each operation taking effect at one instant.

**The judgement to demonstrate: pick per operation, not per system.**

| Operation                          | Model needed     | Why                                                  |
| ---------------------------------- | ---------------- | ---------------------------------------------------- |
| Browsing the catalog               | Eventual         | Seconds of staleness harms nobody                    |
| Viewing your own just-placed order | Read-your-writes | Otherwise the retailer thinks it failed and reorders |
| Feed comments                      | Causal           | A reply before its parent is confusing               |
| Decrementing stock at checkout     | Strong           | Anything less means overselling                      |
| Credit limit check                 | Strong           | Anything less means over-extending credit            |
|                                    |                  |                                                      |

**Interview line:** *"I'd pick the model per operation. Catalog browsing is eventually consistent, order history needs read-your-writes, and stock and credit checks need strong consistency because the cost of being wrong is real money."*

## 46. Two-phase commit · T2

**What it is.** A coordinator asks every participant "can you commit?", and if all say yes, tells them all to commit.

**Why people avoid it, and you should be able to say this:** it holds locks across the network for the whole protocol, the coordinator is a single point of failure, and **if the coordinator crashes during the commit phase, participants are stuck holding locks waiting for an answer that never comes.** It trades availability for consistency in exactly the way a high-throughput system can't afford.

**Interview line:** *"2PC is a blocking protocol with a single point of failure — a coordinator crash leaves participants holding locks indefinitely. That's why sagas exist. But first I'd ask whether the operation needs to span services at all, because one transaction in one database is simpler and more correct than any saga."*

## 47. Sagas · T1

**What it is.** A multi-step business operation spread across services or resources that can't share one database transaction. Each step is its own local transaction, and each has a **compensating action** that undoes it if a later step fails.

**Why they exist.** The moment an operation spans two databases, you have no `BEGIN`/`COMMIT` covering both. Two-phase commit (#46) technically solves it but blocks and has a coordinator single point of failure. A saga trades atomicity for availability: the operation is no longer all-or-nothing in an instant, it's all-or-nothing *eventually*, and intermediate states are visible along the way.

**The order saga, concretely:**

| Step | Local transaction                       | Compensation            |
| ---- | --------------------------------------- | ----------------------- |
| 1    | Reserve inventory                       | Release reservation     |
| 2    | Reserve credit / authorise payment      | Void authorisation      |
| 3    | Create order, confirm to retailer       | Cancel order            |
| 4    | Notify distributor, schedule fulfilment | Cancel with distributor |

If step 3 fails, you run compensations for 2 and 1, in reverse order.

## Orchestration vs choreography

**Orchestration** — one coordinator service owns the workflow. It calls step 1, waits, calls step 2, and on failure runs the compensations itself. The workflow lives in one readable place.

**Choreography** — no coordinator. Each service listens for events and reacts. Inventory hears `OrderRequested` and emits `InventoryReserved`; payment hears that and emits `PaymentAuthorised`; and so on. Failures emit `*Failed` events that other services listen for and compensate against.

|                   | Pros                                                                                                                | Cons                                                                                                                                                                                         |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Orchestration** | The whole workflow is readable in one file. Easy to monitor, easy to see where a saga is stuck. Easy to add a step. | The orchestrator couples to every participant and can grow into a god service. It's a dependency for every flow.                                                                             |
| **Choreography**  | Maximum decoupling; services only know events. Adding a listener needs no central change.                           | **Nobody can tell you what the workflow is without reading every service.** Debugging a stuck saga means tracing events across six logs. Cyclic event chains are easy to create by accident. |

**The answer that scores:** *"For anything business-critical with compensations, I'd orchestrate. Choreography is more elegant on a whiteboard, but when a saga is stuck at 2am you need one place that knows what step it's on. Observability of the workflow beats architectural purity."*

## The saga state machine

A saga needs durable state — you can't hold it in memory, because the process running it will be redeployed mid-flight. So the orchestrator persists a row per saga instance:

`saga_id, order_id, current_step, status, started_at, updated_at, last_error, attempt_count`

Status moves through something like `running → compensating → compensated` or `running → completed`. **Transitions are validated** — a late response for step 2 can't move a saga that's already compensating back to running.

**This is the same state-machine discipline you applied at Kazam**, and it's worth saying so: the thing that makes a long-running distributed workflow debuggable is that its state is a row you can query, not a call stack that died with the process.

## The property sagas lose, and almost nobody mentions

A database transaction gives you **A**tomicity, **C**onsistency, **I**solation and **D**urability. A saga gives you atomicity (eventually) and durability. **It does not give you isolation.**

That means other transactions can see the intermediate states. Concretely: between "inventory reserved" and "payment authorised," another part of the system can read a stock count that reflects a reservation for an order that's about to be cancelled. Someone looking at a report sees an order that will shortly not exist.

**The mitigations, and naming them is a real seniority signal:**

- **Semantic lock** — mark the record as in-progress (an order in `pending`, a reservation with an expiry) so readers know it isn't final and can choose to ignore or display it differently.
- **Commutative updates** — design the operations so order doesn't matter. Increment/decrement commute; a blind `SET` doesn't.
- **Pessimistic view** — show the conservative number. Report available stock as if every pending reservation will succeed, so you never oversell on the back of a saga that's mid-flight.
- **Re-read and re-validate at the pivot** — before the point of no return, check the assumptions still hold.

**Interview line:** *"The thing people forget about sagas is that you lose isolation, not just atomicity. Intermediate states are visible, so you need semantic locks — an order in pending state, a reservation with an expiry — so the rest of the system knows that data isn't final yet."*

## The pivot transaction

Order your steps so that **everything reversible happens first and the irreversible step happens last.** The irreversible step is the **pivot** — after it, the saga must roll *forward*, not back.

In the order saga, actually dispatching goods from the distributor's warehouse is a pivot. Before it, cancelling is cheap. After it, "cancelling" means a return, a credit note and reverse logistics — which is a completely different and much more expensive workflow.

**Designing step order deliberately is the cheapest reliability win in saga design**, because every step you move before the pivot is a failure that costs you nothing.

| Pros of sagas                                         | Cons                                             |
| ----------------------------------------------------- | ------------------------------------------------ |
| Works across services with no distributed transaction | Intermediate states are visible — no isolation   |
| Each step is a simple local transaction               | Every compensation must be written and tested    |
| No locks held across the network, so it scales        | Debugging a half-finished saga is genuinely hard |
| Failure handling is explicit rather than hoped-for    | Significantly more code than one transaction     |

**The judgement line, and it's one of the best answers available to you:** *"At this scale I'd keep order, inventory and payment in one service and one database, so the whole thing is a single Postgres transaction and I don't need a saga at all. Sagas are what you reach for once you've already split those services — and I'd want a strong reason to split them first, because a transaction is simpler and more correct than any saga I can write."*

**Full treatment of the rollback half is §80 — it's the part interviews actually drill.**


## 48. Idempotency · T1

**What it is.** Doing the operation five times has the same effect as doing it once.

**Why it's mandatory.** A timeout tells you nothing, so clients retry, so duplicates happen. There's no way out of that chain.

**Especially here:** your users are on patchy networks and will tap "Place Order" repeatedly on a frozen screen. **Duplicate submission is the normal case, not the exception.**

**How to build it:**

1. The client generates a key per logical intent — the same key on every retry of that attempt.
2. A table with a **unique constraint** on the key.
3. `INSERT ... ON CONFLICT DO NOTHING`. If you inserted the row, you own the operation. If zero rows, someone else does — return their stored response, or 409 if still in flight.

**The critical detail: the database's unique constraint decides the winner, not your application code.** "Check if it exists, then insert" is a TOCTOU race — two pods both pass the check in the same millisecond. Interviewers listen for exactly this mistake.

**And:** a duplicate returns the **stored original response**, not a re-run. Idempotent means "same answer," not just "no double damage."

| Pros | Cons |
|---|---|
| Makes retries safe, which makes everything else possible | An extra table and an extra write per request |
| Handles double-taps, network retries, duplicate webhooks | Keys need expiry or the table grows forever |
| Required for at-least-once messaging to work at all | Clients must generate and reuse keys correctly |

**Interview line:** *"This is the work I did at Kazam. Client-supplied key, unique constraint in the database doing the arbitration, stored response returned on duplicate. The thing I'd never say is that I checked and then inserted — that's a race."*

## 49. Distributed locks and fencing tokens · T2

**What it is.** Making sure only one process does something at a time across many machines.

**The Redis implementation:** `SET key <random-token> NX PX <ttl>` — atomic acquire with a TTL so a crashed holder can't deadlock everything. Release with a **Lua script that checks the token matches before deleting**, so you never delete someone else's lock after your own TTL expired.

**The honest caveat that marks you as careful:** **Redis locks are not safe for correctness-critical mutual exclusion.** The Redlock algorithm is disputed. Under a GC pause or clock skew, your TTL can expire while you still think you hold the lock, and two holders both proceed.

**Fencing tokens** are the fix: the lock hands out a monotonically increasing number, and **the resource itself rejects any write with a token lower than the highest it has seen.** Now a stale lock holder is harmless, because its write is rejected.

**The rule to state:** *"using a Redis lock to avoid duplicate work is fine. Using one to guarantee a payment happens once is not — that's what a database unique constraint is for."*

**Interview line:** *"Distributed locks are an optimisation, not a correctness mechanism. If correctness depends on it, I want a database constraint or a fencing token checked by the resource, because a lock can expire while the holder still believes it owns it."*

## 50. Leader election and consensus · T3

**What it is.** How a cluster agrees on one value or one leader despite failures. **Raft** and **Paxos** are the algorithms.

**Why you care:** you almost never implement this, but you use it constantly — etcd, Kafka's controller, Postgres failover tooling, and any distributed lock that's actually safe.

**The thing worth knowing:** consensus needs a **quorum** — a majority. That's why clusters have odd numbers of nodes (3, 5): with 3 you can lose 1, with 5 you can lose 2. An even number buys you nothing extra and risks a split vote.

**Interview line:** *"I'd use something that implements Raft rather than implement it. The practical consequence is odd-numbered clusters, because consensus needs a majority."*

## 51. Clocks and logical clocks · T2

**The rule: never order distributed events by wall-clock time.** NTP drift, leap seconds and VM pauses make "last write wins by timestamp" a data-loss mechanism — two servers can disagree by seconds, and the wrong write wins silently.

**Example.** A distributor's system and yours both report an order status with their own timestamps. Their clock is 4 seconds fast. You apply updates in the wrong order and an order shows "dispatched" after "delivered."

**The alternatives:** **Lamport timestamps** (a counter giving you a consistent ordering), **vector clocks** (which can detect that two writes were genuinely concurrent rather than ordered), **sequence numbers from a single authority**, or a **state machine that rejects illegal transitions** regardless of claimed order.

**That last one is your approach and it's the most practical.** You don't need to know the true order if "completed → in_progress" is simply not a legal move.

**Interview line:** *"I don't trust timestamps from systems I don't control. I use sequence numbers where the provider gives them, and a state machine that rejects illegal backwards transitions — so a late webhook can't undo a completed order regardless of what its timestamp claims."*

## 52. Distributed ID generation · T2

**What it is.** Generating unique IDs across many servers without coordinating.

| Option               | Pros                                                      | Cons                                                                                                         |
| -------------------- | --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **Auto-increment**   | Simple, small, sortable                                   | Needs one database; leaks volume to competitors; blocks sharding                                             |
| **UUID v4 (random)** | No coordination; generate anywhere                        | 16 bytes; **random order destroys B-tree index locality** — inserts scatter across the index and fragment it |
| **UUID v7 / ULID**   | Time-ordered *and* unique, so index locality is preserved | Slightly leaks creation time                                                                                 |
| **Snowflake**        | Time-ordered, compact, encodes machine ID                 | Needs machine-ID coordination and decent clocks                                                              |

**The insight most candidates miss, and it's a genuinely good one to raise:** random UUIDs as a primary key hurt write performance at scale. Every insert lands at a random point in the B-tree, so you're constantly touching cold pages and fragmenting the index. **Time-ordered IDs (UUID v7, ULID, Snowflake) keep inserts appending to the hot end**, which is dramatically better.

**And the business point:** sequential integer IDs in public URLs tell a competitor exactly how many orders you process. `order/1042` today and `order/1536` next week is your weekly volume.

**Interview line:** *"I'd use time-ordered IDs — UUID v7 or ULID — rather than random UUIDs, because random keys scatter inserts across the B-tree and fragment the index. And I wouldn't expose sequential integers publicly, because that leaks volume."*

---

# Group 7 — Reliability

## 53. Timeouts, retries, backoff, jitter · T1

**The four together, because they only work together.**

**Timeouts.** Every network call, always. Derive the value from the downstream's actual latency distribution, not a round number. **A missing timeout is the single most common cause of cascading failure** — without one, a hung dependency holds your connections and threads until you run out, and then *unrelated* requests start failing too.

**The subtle one worth raising:** your timeout should be **shorter** than your caller's. If your caller gives up after 3 seconds and you keep working for 10, you're spending capacity on a response nobody will read, while new requests queue behind it.

**Retries.** Only for **idempotent** operations, or non-idempotent ones carrying an idempotency key. Retrying a non-idempotent charge is how you double-bill someone.

**Exponential backoff.** Wait 1s, 2s, 4s, 8s — so you don't hammer a struggling service.

**Jitter.** Add randomness to the backoff. **Without it, all your clients retry at exactly the same moment**, creating a synchronised thundering herd that re-kills the service the instant it recovers. Jitter is one line of code and it's the difference between recovery and a retry storm.

**Also:** cap total attempts. Infinite retries turn a transient blip into a permanent self-inflicted outage.

| Pros                                                     | Cons                                                       |
| -------------------------------------------------------- | ---------------------------------------------------------- |
| Handles the transient failures that dominate in practice | Amplifies load exactly when the system is weakest          |
| Invisible to users when it works                         | Retrying non-idempotent operations duplicates side effects |
| Cheap to implement                                       | Masks a real problem until it's severe                     |

**Interview line:** *"Timeouts on everything, shorter than my caller's. Retries only on idempotent operations, with exponential backoff and jitter and a cap. Jitter especially — without it every client retries in lockstep and you re-kill the service the moment it comes back."*

## 54. Circuit breaker · T1

**What it is.** Track the failure rate to a dependency. Past a threshold, **stop calling it entirely** for a cooldown — fail fast instead of queuing requests against a dead service. Then let a trickle of probe requests through to test recovery.

**Three states:** **Closed** (normal, calls pass through), **Open** (failing fast, no calls), **Half-open** (a few probes allowed; success closes it, failure re-opens).

**Example.** A distributor's API goes down. Without a breaker, every order to that distributor waits for the full timeout, your threads fill up, and **orders to healthy distributors start failing too.** With a breaker, calls to the broken one fail instantly, you queue the work for later, and the rest of the platform is unaffected.

**The insight to state:** **when a dependency is down, retrying makes it worse. Failing fast is the cooperative behaviour** — it gives the struggling service room to recover instead of piling on.

| Pros                                                 | Cons                                                     |
| ---------------------------------------------------- | -------------------------------------------------------- |
| Stops one bad dependency taking down everything      | Another thing to tune; bad thresholds cause false trips  |
| Gives the failing service room to recover            | Can mask a problem if nobody's alerting on open breakers |
| Fails fast instead of making users wait for timeouts | Needs a sensible fallback for the open state             |

**Interview line:** *"A circuit breaker per distributor, so one partner being down fails fast instead of consuming my thread pool and taking out orders for everyone else. When a breaker opens I'd queue the work and alert, not drop it."*

## 55. Bulkhead · T2

**What it is.** Named after ship compartments. Isolate resources per dependency so one failure can't consume everything.

**Example.** You have a pool of 100 worker threads shared across all distributor calls. One distributor hangs, and all 100 threads end up waiting on it — now *every* distributor's orders are stuck. With bulkheads, each distributor gets a cap of 10 threads. The broken one consumes its 10 and stops.

**Applies to:** thread pools, connection pools, rate limits per tenant, and separate service instances for critical vs non-critical paths.

**Interview line:** *"Per-dependency concurrency limits so one slow partner can't eat the whole worker pool. The circuit breaker stops the calls; the bulkhead limits the damage before the breaker trips."*

## 56. Load shedding and admission control · T2

**What it is.** When you're over capacity, **reject work rather than accept it into an unbounded queue.**

**The queueing theory point, which is worth stating:** as utilisation approaches 100%, latency goes to infinity. This isn't gradual — it's a cliff. **That's why systems must run with headroom**, typically targeting 60–70% utilisation rather than 90%.

**How to shed well:** reject with `429` and a `Retry-After`. Shed by priority — drop analytics writes before order placements. Drop requests that have already exceeded their deadline, since nobody's waiting for them.

**Interview line:** *"Under overload I'd shed load by priority rather than degrade uniformly — an order placement is worth more than an analytics event. A bounded queue with shedding degrades gracefully; an unbounded one collapses."*

## 57. Rate limiting · T1

**What it is.** Capping how many requests a client can make in a window.

**Why you need it:** one buggy client, one scraper, or one retailer's app stuck in a retry loop can consume capacity meant for everyone.

**Where it goes:** at the edge, and **in Redis, not in process memory** — otherwise your limit multiplies by instance count and changes on every deploy.

| Algorithm                  | Pros                                         | Cons                                     |
| -------------------------- | -------------------------------------------- | ---------------------------------------- |
| **Fixed window**           | Simplest                                     | Allows a 2x burst at the window boundary |
| **Sliding log**            | Exact                                        | Stores every timestamp — memory-heavy    |
| **Sliding window counter** | Good accuracy, cheap                         | Slightly approximate                     |
| **Token bucket**           | Allows controlled bursts, matches real usage | Two parameters to tune                   |

**The product-sense point, and it's a strong one here:** limits for this user base should be **generous**, and always return `429` with `Retry-After` rather than dropping the connection. These clients are retry-heavy **by necessity, not by abuse**. Punishing a retailer on a bad connection for retrying is punishing them for their network.

**Interview line:** *"Token bucket in Redis at the gateway, with generous limits and a proper `Retry-After`, because retries here are a symptom of bad connectivity rather than abuse. I'd rate-limit abusive patterns separately from normal retry behaviour."*

## 58. Graceful degradation and fallbacks · T1

**What it is.** When part of the system fails, serve something useful instead of an error.

**Examples:** recommendation service down → show the catalog unranked. Search cluster down → fall back to a simple database query with no typo tolerance. Credit service slow → let retailers with plenty of headroom through on a cached limit, but **block anyone near their limit.**

**That last one is the example to give**, because it shows you degrade *differently based on risk* rather than treating the system as one on/off switch.

**The rule to state:** *"browsing should survive almost any failure. Order placement should fail loudly rather than quietly accept an order we can't fulfil — a false yes is worse than an honest error."*

| Pros | Cons |
|---|---|
| Partial outages don't become total outages | More code paths, and they're rarely tested |
| Users often don't notice | Degraded mode can hide a real outage from you |
| Buys time to fix things properly | Needs an explicit decision per feature |

**Interview line:** *"I'd decide per feature what degradation looks like, and I'd alert when we enter degraded mode — the danger is silently running degraded for a week because nobody noticed."*

## 59. Health checks: liveness vs readiness · T2

**Two different questions, and conflating them causes real outages.**

**Liveness** — "is this process alive?" If it fails, the orchestrator **kills and restarts** the container.

**Readiness** — "can this instance serve traffic right now?" If it fails, the load balancer **stops sending traffic** but doesn't restart it.

**Why the distinction matters.** If your liveness check also tests the database connection, then a database blip **restarts every container simultaneously** — turning a brief database issue into a full outage, and the restart storm makes recovery slower. Liveness should only check that the process itself isn't wedged. Dependency checks belong in readiness.

**Also:** readiness lets a starting instance warm caches and open connection pools before receiving traffic, which prevents the first few hundred requests after a deploy from timing out.

**Interview line:** *"Liveness checks only that the process isn't deadlocked; readiness checks dependencies. Putting a database check in liveness means a database blip restarts your whole fleet at once."*

## 60. Redundancy, failover, RPO and RTO · T2

**The two numbers that define your disaster recovery, and you should know the words:**

- **RPO — Recovery Point Objective.** How much data you can afford to lose. "15 minutes" means backups or replication must be at most 15 minutes behind.
- **RTO — Recovery Time Objective.** How long you can afford to be down.

**Example.** For order and ledger data, RPO should be near zero — losing an hour of orders means money you can't account for. For a derived search index, RPO can be hours, because you can rebuild it from Postgres.

**The rule nobody follows until it bites them: a backup you haven't restored is not a backup.** Test the restore on a schedule. Plenty of companies have discovered their backups were empty at the worst possible moment.

**Failover:** automatic is fast but risks **split-brain** (two nodes both believing they're the primary, both accepting writes). Manual is safer and slower. Most teams use automatic with a fencing mechanism.

**Interview line:** *"I'd set RPO near zero for the ledger and order data, and hours for anything derived that I can rebuild. And I'd schedule restore drills, because an untested backup is a guess."*

## 61. Multi-AZ vs multi-region · T2

**Multi-AZ** means several data centres in one region, a few milliseconds apart. **Multi-region** means geographically separate, tens to hundreds of milliseconds apart.

**Multi-AZ is nearly free and you should always do it** — synchronous replication across AZs costs a few milliseconds and protects against a whole data centre failing.

**Multi-region is a different scale of problem.** Cross-region latency makes synchronous replication impractical, so you either accept async replication (and data loss on failover) or multi-leader writes (and conflict resolution, which is genuinely hard).

**The judgement call for this business:** *"Kirana Club's users are all in India, so multi-region buys me disaster recovery, not latency. I'd run multi-AZ for availability and keep cross-region backups for DR, rather than taking on multi-region writes and conflict resolution for a problem we don't have."*

That's a good answer because **the expected move is to say "multi-region for availability" and declining it with a reason shows judgement.**

## 62. Chaos engineering · T3

**What it is.** Deliberately breaking things in production, under controlled conditions, to find out whether your resilience actually works.

**The honest point:** every failure path you've written is untested code until something exercises it. Your circuit breaker, your fallback, your retry logic — all of it is theory until a failure happens.

**Interview line:** *"Failure paths are the least-tested code in any system. Even without a full chaos practice, I'd want game days where we kill a dependency in staging and check the degradation actually works."*

---

# Group 8 — Delivery and operations

## 63. Deployment strategies · T2

| Strategy       | How it works                                       | Pros                                       | Cons                                                |
| -------------- | -------------------------------------------------- | ------------------------------------------ | --------------------------------------------------- |
| **Rolling**    | Replace instances a few at a time                  | No extra infrastructure; the default       | Both versions run at once — needs compatible schema |
| **Blue-green** | Two full environments, switch traffic              | Instant rollback; only one version live    | Double infrastructure; database is still shared     |
| **Canary**     | Send 1% of traffic to the new version, watch, ramp | Catches problems with minimal blast radius | Needs good metrics and traffic splitting            |

**The point people miss: none of these protect you from a bad database migration.** Blue-green gives you instant application rollback, but if the new version already dropped a column, rolling back the code doesn't bring it back. **Schema changes need expand/contract regardless of deployment strategy.**

**Interview line:** *"Rolling by default, canary for anything touching the order path. But the deployment strategy doesn't save you from a bad migration — that needs expand/contract, because a rollback can't undo a dropped column."*

## 64. Feature flags · T2

**What it is.** Shipping code that's switched off, and turning it on separately from deploying it.

**What they give you:** deploy and release become separate decisions; a bad feature is turned off in seconds rather than needing a rollback; percentage rollouts; and per-tenant enablement, which matters when you want one distributor to trial something.

**The cost, and you should name it:** every flag is a branch, and **two flags means four code paths you probably aren't testing.** Flags need expiry dates and someone to clean them up, or your codebase becomes an unreadable thicket of conditionals.

**Interview line:** *"Flags separate deploy from release, which is what lets you ship on a Friday. But they're debt with a half-life — I'd put an expiry on each one, because a codebase with fifty stale flags has more untested combinations than tests."*

## 65. Expand/contract migrations · T1

**What it is.** Changing a database schema without downtime, given that during a rolling deploy **old and new code run simultaneously against one schema.**

**The four steps:**

1. **Expand** — add the new column as nullable. Old code ignores it; new code can use it.
2. **Backfill** — populate in batches, never one giant `UPDATE` that locks the table.
3. **Migrate** — deploy code that writes both columns and reads the new one.
4. **Contract** — once nothing reads the old column, drop it.

**A rename is three deploys, not one edit.**

**The specific things that will lock a live table:**

- `ALTER TABLE ... ADD COLUMN ... NOT NULL DEFAULT ...` on a large table in older Postgres versions — it rewrites every row.
- `CREATE INDEX` without `CONCURRENTLY` — blocks writes for the duration.
- Adding a foreign key without `NOT VALID` then validating separately — scans and locks.
- Any long transaction holding a lock while other queries queue behind it.

**Interview line:** *"Expand/contract, always, because during a rolling deploy both versions are live against one schema. And indexes get built `CONCURRENTLY` — a plain `CREATE INDEX` on a live orders table blocks writes and looks exactly like an outage."*

## 66. Autoscaling · T2

**What it is.** Adding and removing instances automatically based on load.

**Reactive** scales on a metric — CPU, request rate, queue depth. **Predictive/scheduled** scales ahead of known patterns.

**The failure modes to name:**

- **Scaling on the wrong metric.** CPU is a poor proxy for an I/O-bound service that's slow because the database is slow. Adding instances then makes the database *worse*. **Queue depth or request latency is usually the better signal.**
- **Scaling too slowly.** If an instance takes 3 minutes to start and your spike lasts 2 minutes, autoscaling does nothing. Pre-warm for predictable events.
- **Thrashing** — scaling up and down repeatedly. Needs cooldowns.
- **Scaling the app into a database limit.** More app instances means more connections, which is how you exhaust Postgres. PgBouncer first.

**For a flash sale, scheduled scaling beats reactive**, because you know when it starts and reactive scaling is always behind the curve.

**Interview line:** *"I'd scale on queue depth or latency rather than CPU, and I'd pre-scale for known events rather than relying on reactive scaling, which is always a few minutes behind the spike. And I'd make sure scaling the app doesn't just exhaust the database connection pool."*

## 67. Capacity planning and load testing · T2

**What it is.** Knowing your limits before your users find them.

**The method:** load test to find where latency degrades — not where it crashes, but where p99 starts climbing. That's your real capacity. Then plan to run at 60–70% of it, because of the utilisation cliff.

**The rule that matters:** **load test against production-like data volumes.** A query that's fast against 10,000 rows can be catastrophic against 10 million, because the planner switches strategies. Testing against a small dataset tells you almost nothing.

**Interview line:** *"Load test against production-scale data, not production-scale traffic alone — the plan flip when a table grows past a threshold is what actually bites you, and it's invisible on a small dataset."*

## 68. Observability · T1

**What it is.** Being able to answer "why is this slow / wrong / broken" without shipping new code to find out. Monitoring tells you *that* something is wrong; observability lets you work out *why*.

**The three pillars, and what each is actually for:**

| Pillar | Answers | Cost shape |
|---|---|---|
| **Metrics** | "Is something wrong, and how bad?" | Cheap — numbers aggregated over time |
| **Traces** | "Where in the request did the time go?" | Medium — sampled |
| **Logs** | "What exactly happened to this one request?" | Expensive — volume scales with traffic |

**The workflow they support together:** a metric alerts you (error rate on `POST /orders` jumped). A trace shows you where (the credit-check call to the payments service is taking 4 seconds). Logs tell you why (connection pool exhausted, every acquire timing out). **If you can describe that flow — alert, trace, log — you've shown you've actually debugged something in production.**

**Metrics: RED and USE.**

- **RED** per endpoint — **R**ate, **E**rrors, **D**uration. The service-level view.
- **USE** per resource — **U**tilisation, **S**aturation, **E**rrors. The infrastructure view.

**Two things that mark experience:**

**Alert on symptoms, not causes.** Alert on error rate and latency, not CPU. Users feel the former. A CPU alert at 3am that corresponds to no user impact is how teams learn to ignore alerts.

**Percentiles, never averages.** The mean hides everything. p99 is where your worst-served customers live. And **a p99 computed per instance and then averaged across instances is mathematically wrong** — you need histograms aggregated properly, which is what `histogram_quantile` over a Prometheus histogram does. Knowing that averaging percentiles is invalid is a genuine depth signal.

**The business-metric point, which is the best thing you can say here:** alert on **orders per minute** too. A broken deploy that returns `200` with an empty catalog looks perfectly healthy on every infrastructure dashboard — CPU normal, error rate zero, latency fine. The only thing that catches it is the business metric falling off a cliff.

**Interview line:** *"Metrics to know something's wrong, traces to find where, logs to find why. Alerts on symptoms rather than CPU, percentiles rather than averages, and a business metric like orders per minute — because a deploy that returns 200 with an empty response is invisible to every technical signal."*

**Full treatment of tracing is §81 and of logging is §82.**


## 69. SLI, SLO and error budgets · T2

- **SLI** — the thing you measure. "Share of order requests that succeed in under 500ms."
- **SLO** — your target. "99.9% of them."
- **Error budget** — what the SLO allows you to fail. 99.9% means 0.1% can fail; that's your budget.

**Why the error budget idea is useful**, and it's a good thing to raise in a prioritisation discussion: it turns "should we ship fast or be reliable" from an argument into arithmetic. Budget remaining → ship. Budget spent → stop shipping features and fix reliability. **It gives engineering and the business one shared number instead of two opinions.**

**And: 100% is the wrong target.** Chasing it costs enormously and users can't tell the difference, because their own mobile network is less reliable than your service.

**Interview line:** *"Error budgets turn the speed-versus-reliability argument into a number both sides agree on. And 100% is the wrong goal — for users on 3G, the marginal reliability is invisible to them and expensive to us."*

## 70. Cost as a design constraint · T2

**Why it's a real engineering concern**, especially here: Kirana Club serves price-sensitive retailers on thin margins. **Infrastructure cost per order is a unit-economics number**, not just an ops concern.

**The big levers:** CDN offload rather than serving from your app; right-sizing instances instead of leaving the defaults; lifecycle rules moving cold data to cheap storage; caching reducing database size and therefore instance cost; and watching **cross-AZ and egress data transfer**, which is a surprisingly large and invisible line item.

**The SMS point from the notification section belongs here too:** at millions of users, choosing push over SMS is a six-figure decision.

**Interview line:** *"I'd treat cost per order as a metric alongside latency. At this user base's margins, infrastructure cost is part of the unit economics — and choosing push over SMS for notifications is a bigger financial decision than most architecture choices."*

---

# Group 9 — Search, geo and ranking

## 71. Inverted index and search ranking · T2

**What it is.** A normal index maps a row to its contents. An **inverted index** maps each word to the list of documents containing it. That's how search engines return results for a word in milliseconds across millions of documents.

**Example.** Searching "parle biscuit" looks up "parle" → [doc 4, 19, 203] and "biscuit" → [doc 19, 88, 203], intersects them, and ranks the results.

**Ranking basics worth knowing by name:** **TF-IDF** (a word matters more if it's frequent in this document and rare across all documents) and **BM25**, the modern refinement that's the default in Elasticsearch. **You don't need the maths — you need to know the names and that relevance is tunable.**

**In a commerce context, pure text relevance isn't enough.** You boost by availability (never rank an out-of-stock SKU first), by how often this retailer has bought it, by margin, and by whether a distributor who serves their area actually carries it. **Saying that search ranking in commerce is a business problem, not just a text problem, is the thing that lands.**

**Interview line:** *"I'd start with Postgres full-text and a GIN index, because it's zero new infrastructure and handles the common cases. I'd move to Elasticsearch for typo tolerance and synonyms — and for a user base typing product names in Hindi, English and Hinglish transliteration, that's probably sooner rather than later. But ranking is where the value is, and that's a business question: availability and purchase history should outrank text relevance."*

## 72. Geospatial indexing · T2

**What it is.** Answering "what's near me" efficiently. **You've built this** — Pujo Atlas, PostGIS, sub-200ms proximity search.

**Why a normal index doesn't work.** A B-tree indexes one dimension. Location is two. You can't sort latitude and longitude into one order that keeps nearby things nearby.

**The approaches:**

- **Geohash** — encode lat/long into a string where shared prefixes mean nearby. Simple, works with any string index. Weakness: two points can be very close but sit either side of a grid boundary and share no prefix.
- **Quadtree** — recursively subdivide space, splitting dense areas further. Adapts to uneven density.
- **S2 / H3** — Google's and Uber's cell systems. Better boundary behaviour.
- **PostGIS with a GiST index** — what you used. A `geography` column and `ST_DWithin` for radius queries.

**The detail that proves you built it rather than read about it:** **`ST_DWithin` can use the index; computing `ST_Distance` for every row and filtering cannot.** One scans an index, the other scans the table.

**Where it applies at Kirana Club:** distributor serviceability (which distributors deliver to this pincode), delivery routing and clustering, and territory assignment for field staff.

**Interview line:** *"I built this on Pujo Atlas — PostGIS with a GiST index on a geography column and `ST_DWithin` for radius queries, because `ST_DWithin` uses the index while computing distance per row and filtering doesn't. Here it'd apply to distributor serviceability by pincode and to delivery clustering."*

## 73. Recommendations and cold start · T3

**The approaches, briefly.** **Collaborative filtering** — "retailers like you also bought X." **Content-based** — "similar to what you bought." **Popularity** — "top sellers in your area," which is the honest baseline.

**The cold-start problem:** a brand-new retailer has no history, so personalisation has nothing to work with.

**The answer that actually scores here:** *"For a B2B grocery platform, the highest-value recommendation isn't a clever model — it's the retailer's own reorder list. They buy roughly the same things on a cycle. 'Reorder your last order' and 'you usually buy this every 12 days, it's day 14' will beat a collaborative filtering model for a long time, and I can ship it this week."*

That's a strong answer because **it declines the fancy solution with a domain reason**, which is exactly the judgement axis.

## 74. A/B testing infrastructure · T3

**What it is.** Splitting users into groups, showing them different things, and measuring the difference.

**What matters technically:** stable assignment (a user must stay in the same group across sessions — hash the user ID, don't randomise per request), a holdout group, and running long enough to reach significance.

**The point to make:** *"I'd want any retention or AOV feature shipped to a percentage with a holdout, because otherwise we can't tell whether it worked or whether it was seasonal."*

---

# Group 10 — Security at scale

## 75. Authentication and authorisation · T1

**Authentication** is who you are. **Authorisation** is what you may do.

**JWT in practice.** A short-lived token carrying identity, tenant and scopes, signed by the server, validated at the gateway and passed inward. Services trust the gateway's verdict rather than each re-validating.

**The trade-off you must know:** JWTs are stateless and therefore fast and scalable, but **you cannot revoke one before it expires** without reintroducing state. Which is why access tokens are short-lived (minutes) with a revocable refresh token behind them.

**The mobile-specific point for this product:** retailers on bad connections shouldn't be logged out constantly. Long-lived refresh tokens with silent renewal, and a session that survives network interruption. **Security that makes the app unusable on 3G is a product failure.**

**Interview line:** *"Short-lived access tokens validated at the gateway with a revocable refresh token behind them, because you can't revoke a JWT mid-life. And generous refresh windows, because forcing a re-login on a retailer with patchy connectivity is a worse outcome than the marginal security gain."*

## 76. RBAC and ABAC · T2

**RBAC** — roles hold permissions, users hold roles. Simple and usually enough.

**ABAC** — decisions based on attributes: "a distributor's manager can view orders where the distributor matches theirs **and** the order is under ₹50,000." More expressive, harder to reason about and audit.

**The point that matters:** **where the check happens.** Middleware guards the endpoint. **Only a check in the data layer guards the rows.** In a multi-tenant system you need both, because a properly authenticated user of tenant A must still never reach tenant B's data.

**Interview line:** *"RBAC unless the business genuinely needs attribute conditions. And the check belongs in the data layer, not just middleware — an endpoint check tells you the user may call this API, not that they may see this row."*

## 77. Multi-tenancy isolation · T1

| Model | Pros | Cons |
|---|---|---|
| **Shared schema, `tenant_id`** | Cheapest. One migration. Scales to many tenants. | One missing `WHERE tenant_id` is a data breach. Noisy neighbours. |
| **Schema per tenant** | Real separation; per-tenant customisation. | Every migration becomes N migrations. Strains past a few hundred. |
| **Database per tenant** | Strongest isolation; per-tenant backup/restore. | High operational cost per tenant. |

**How to prevent leakage — layered, and this is the answer they want:**

1. **Postgres Row-Level Security**, so the database enforces it even when application code forgets. **Most candidates never mention this.**
2. A mandatory data-access layer injecting the tenant filter, so an unscoped query is impossible to write.
3. Tenant resolved once per request from the **signed token**, never a client-supplied header.
4. **Tests that assert tenant A cannot read tenant B's rows.** Test the attack, not just the happy path.

**Interview line:** *"I've built both models — shared schema at Kazam, schema-per-tenant with django-multitenants at Alemeno. For hundreds of distributors I'd use shared schema with Row-Level Security, because schema-per-tenant turns every migration into N migrations. RLS gives database-enforced isolation without the migration tax."*

## 78. Encryption and PII · T2

**In transit** — TLS everywhere, mTLS internally if the threat model justifies it. **At rest** — disk encryption is table stakes; **column-level encryption** for the genuinely sensitive fields.

**PII in this product:** phone numbers, shop addresses, GST numbers, credit history. Phone numbers especially are both PII and your primary identifier.

**The practical rules:** mask PII in logs (a correlation ID in logs, never a phone number); restrict who can query it; have a deletion path, because DPDP in India requires it; and tokenise payment details rather than storing them — let the payment provider hold the card.

**Interview line:** *"Phone numbers are PII and they're also our login identifier, so they're in a lot of places. I'd mask them in logs, keep the raw value in one table with restricted access, and reference it by ID everywhere else."*

## 79. DDoS, WAF and bot protection · T3

**DDoS** — absorbed mostly at the CDN layer, which is one of the under-appreciated reasons to use one. **WAF** — filters common attacks before they reach you. **Bot protection** — matters in commerce because competitors scrape pricing, which is genuinely valuable data in a B2B market.

**Interview line:** *"A CDN absorbs most volumetric attacks. The commerce-specific concern is scraping — our pricing is commercially sensitive, so I'd rate-limit catalog access by account rather than only by IP."*

---


# Group 11 — Deep dives: money, stock, rollback and tracing

The five areas worth going deeper on than anything else in this document. Payments and inventory are where a commerce platform's correctness actually lives, saga rollback is the half of sagas that interviews drill, and distributed logging and tracing are what the JD means by "debug production issues."

## 80. Saga rollback and compensation · T1

Sagas (#47) are easy to describe and hard to get right, and **the rollback half is where the real questions are.** Anyone can say "each step has a compensating action." The follow-ups are what separate people who've built one.

### Compensation is semantic, not literal

You are not undoing the step. You are performing a **new business action that cancels its effect.**

| Step                  | What you can't do         | What you actually do                                           |
| --------------------- | ------------------------- | -------------------------------------------------------------- |
| Sent an SMS           | Un-send it                | Send a correction message                                      |
| Charged a card        | Un-charge it              | Issue a refund (a new transaction, visible on their statement) |
| Decremented stock     | Pretend it never happened | Increment it back, with a movement record showing why          |
| Posted a ledger entry | Edit it                   | Post an opposite entry                                         |
| Dispatched goods      | Un-dispatch               | Reverse logistics, a return, a credit note                     |

**The consequence to say out loud: the customer sees the intermediate state.** A retailer whose order fails at step 3 may already have received an SMS, and will see a charge and a refund on their statement rather than nothing. **That's a business decision, not just a technical one, and it needs product buy-in.**

### The four rules of writing a compensation

**1. Compensations must be idempotent.** The compensation will be retried — the orchestrator crashes mid-rollback and restarts. "Release reservation" must be safe to run five times. Key it on the saga ID or the step ID.

**2. Compensations must not fail permanently.** A failed forward step is fine, you compensate. **A failed compensation leaves the system inconsistent with no automatic way out.** So compensations get retried effectively forever — with backoff, then alerting, then a human. You never give up on a compensation the way you'd give up on a forward step.

**3. Compensations run in reverse order.** Step 4 fails, you compensate 3, then 2, then 1. Running them in forward order can break dependencies — releasing a reservation before voiding the payment that references it leaves a dangling reference.

**4. Compensations must be commutative with concurrent activity where possible.** Between the forward step and its compensation, other things happened. Releasing 5 units of stock should be `available = available + 5`, not `available = <the number I remembered>`. A blind `SET` of a remembered value destroys any concurrent change.

### The hardest question: what if the compensation fails?

This is the one they'll ask, and most candidates have no answer. Say this:

> "A failed compensation is the genuinely bad case, because there's no further automatic recovery. So I treat compensations differently from forward steps. They retry indefinitely with backoff rather than giving up after N attempts. If they're still failing after a threshold, the saga goes into a `compensation_failed` state that **pages a human** rather than being silently dead-lettered. And the saga row holds enough context — which steps succeeded, what the external references were — for a person to finish it manually.
>
> The deeper answer is to design so this is rare: make compensations touch only your own database where you can, and push anything irreversible as late as possible so there's less to undo."

### Backward recovery vs forward recovery

**Backward recovery** is rolling back — undo everything, the operation didn't happen.

**Forward recovery** is pushing through — the operation *will* complete, we just need to retry the failing step until it works, possibly with a human unblocking it.

**After the pivot transaction, forward recovery is your only option.** Once goods are physically on a truck, you don't roll back — you complete the order and handle any problem as a return.

**Choosing between them is a business decision.** For a payment that's authorised but where the distributor can't fulfil, do you cancel (backward) or substitute an equivalent product and complete (forward)? **Forward is often better for the business and harder to build.** Saying that out loud shows you understand it isn't purely a technical choice.

### The saga log

Every step and every compensation writes a durable record **before** it executes and updates it after:

`saga_id, step_name, direction (forward/compensating), status (started/succeeded/failed), attempt, external_ref, error, timestamps`

**Why write before you execute:** if the process dies mid-step, on restart you can see "step 2 started but never recorded completion" and go check the external system before blindly retrying. Without that record you don't know whether the payment was authorised or not — you only know you crashed.

**And the external reference matters enormously.** When you call the payment gateway, store their transaction ID the moment you have it. Without it, a crash leaves you holding money you can't find in order to refund it.

### Timeouts and stuck sagas

A saga can hang because a step never returns. Every saga needs:

- **A per-step timeout** — if step 2 hasn't completed in N minutes, treat it as failed and compensate. But **check the external system first**, because "no response" doesn't mean "didn't happen."
- **A sweeper job** that finds sagas stuck in `running` past a threshold and resolves them.
- **A metric on saga age** — the alert is "sagas older than 10 minutes," which catches problems no error rate will.

### Testing compensations — the point nobody makes

**Compensation code is the least-executed code in your system.** It only runs when something fails, which is rare, which means it's almost always the buggiest code you have. It's the classic "worked in staging, broken in production" surface.

How to actually test it: a test per compensation that runs it twice and asserts the same end state (idempotence); a test that injects failure at every step and asserts the system returns to a clean state; and periodically running a saga to failure deliberately in staging.

**Interview line, and this is the one to have ready:** *"The thing I'd be most careful about is that compensation code is the least-exercised code in the system — it only runs on failure, so it's where the bugs hide. I'd test every compensation for idempotence, inject failure at each step and assert the end state, and treat a failed compensation as a page rather than a dead-letter, because there's no automatic recovery from it."*

| Pros of explicit compensation | Cons |
|---|---|
| Failure handling is designed, not accidental | Roughly doubles the code per step |
| Each compensation is a simple local transaction | Rarely executed, so rarely correct |
| You can reason about every failure point | Users see intermediate states |
| Recoverable by a human from the saga log | Failed compensations have no automatic recovery |

## 81. Distributed tracing · T1

**What it is.** Following one request across every service it touches, and seeing exactly where the time went.

**The problem it solves.** A retailer says "placing an order takes 8 seconds." Your order service logs say it took 300ms. Both are true — the other 7.7 seconds were spread across the gateway, the pricing service, a credit check and a distributor callout. **Without tracing you cannot find that, you can only guess.** With it, you look at one trace and see the credit check took 7 seconds.

### The model: traces and spans

A **trace** is one request's whole journey. A **span** is one unit of work inside it — an HTTP handler, a database query, a call to another service. Spans nest into a tree.

```
trace: place_order                                  [8.0s]
├── span: gateway auth                              [0.02s]
├── span: order-service POST /orders                [7.9s]
│   ├── span: resolve prices (pricing-service)      [0.15s]
│   ├── span: credit check (payments-service)       [7.0s]   ← there it is
│   │   └── span: SELECT credit_limit               [6.9s]   ← and why
│   ├── span: BEGIN / reserve inventory / COMMIT    [0.04s]
│   └── span: insert outbox row                     [0.01s]
└── span: publish OrderPlaced                       [0.03s]
```

**Reading a trace like that out loud in an interview is worth a lot**, because it's exactly what the JD's "debug production issues" line is asking about.

### Trace context propagation — the mechanism

Every service must pass the trace ID along, or the trace breaks into fragments. The standard is the **W3C `traceparent` header**:

`traceparent: 00-<32-hex trace id>-<16-hex parent span id>-01`

Your HTTP clients inject it, your servers extract it, and each service creates child spans under the parent. **The last two hex digits are the sampling flag** — whether this trace is being recorded.

**Where propagation usually breaks, and naming these shows you've done it:**

- **Async boundaries.** A message goes onto a queue and the consumer starts a fresh trace with no link back. Fix: put the trace context *in the message headers* and continue the trace, or at minimum record a span link so the two are associated.
- **Background jobs and cron.** They start their own traces, which is correct, but then you can't connect the scheduled work back to the order that triggered it.
- **Thread or context switches.** In Go, if you drop the `context.Context` you drop the trace. In Node, this is what `AsyncLocalStorage` is for.
- **Third-party calls.** You can't trace inside the distributor's system, but you should still have a span covering the call so you can see their latency.

### Sampling — the trade-off that matters

Tracing every request is expensive in storage and in the overhead of producing it. So you sample.

| Strategy | How it works | Pros | Cons |
|---|---|---|---|
| **Head-based** | Decide at the first service, propagate the decision | Cheap, simple, no buffering | You decide before you know whether the request was interesting — **most errors go unsampled** |
| **Tail-based** | Buffer all spans, decide after the request completes | Keeps every error and every slow request | Needs a collector buffering everything; more infrastructure |
| **Rate-limited per endpoint** | N traces per second per route | Rare endpoints stay visible | Still blind to unsampled errors |

**The practical answer, and it's the one to give:** *"Low head-based sampling for the baseline — one or two percent is plenty to see normal behaviour — plus a rule that always samples errors and anything over a latency threshold. Tail-based sampling does this properly if you can afford the collector. The failure mode to avoid is sampling at 1% uniformly and then discovering your rare 500s were never captured."*

### What to actually instrument

Automatic instrumentation (OpenTelemetry libraries) gives you HTTP in/out and database calls for free — which is most of the value for almost no effort. Add manual spans only for meaningful business operations: "reserve inventory," "resolve price," "run saga step 3."

**Add attributes to spans, not just names**: `retailer_id`, `order_id`, `distributor_id`, `saga_id`. Those are what let you find *this* order's trace instead of scrolling through thousands.

**The cardinality warning:** span attributes are fine with high cardinality (that's the point). **Metric labels are not** — putting `order_id` on a Prometheus metric creates a new time series per order and will take down your metrics system. Knowing that the rule differs between traces and metrics is a real detail.

| Pros | Cons |
|---|---|
| The only practical way to find latency in a distributed system | Needs instrumentation in every service to be useful |
| Shows the actual call graph, including calls you forgot about | Sampling means the request you care about may be missing |
| Connects to logs and metrics via the trace ID | Storage cost grows with traffic |
| Finds N+1 queries instantly — a span repeated 200 times is obvious | Broken propagation gives you confidently wrong pictures |

**Interview line:** *"Tracing is what turns 'the order API is slow' into 'the credit check's query is slow.' I'd use OpenTelemetry with W3C trace context, auto-instrument HTTP and database calls, add manual spans for business operations, and sample low for the baseline but always keep errors and slow requests. The part people get wrong is async boundaries — if you don't carry the trace context into the queue message, the trace stops at the publish."*

## 82. Distributed logging and correlation · T1

**What it is.** Making logs from twenty services across a hundred containers answerable as one story.

### Structured logs, not prose

A log line should be a JSON object with fields, not a sentence. `logger.info("order placed", {order_id, retailer_id, amount_paise, duration_ms})` — not `logger.info(f"Placed order {id} for {name} worth {amt}")`.

**Why it matters:** you can query structured fields. `amount_paise > 100000 AND status = "failed"` is a query. The same information in a sentence requires a regex, and the regex breaks the moment someone rewords the message.

### The correlation ID — the single most important thing here

**Generate one ID at the edge and attach it to every log line in every service for that request.** Then one query returns the complete story of one request across the whole system.

Without it, debugging means opening five services' logs and matching by timestamp and guesswork — which is impossible under load, because a hundred other requests are interleaved.

**In practice, use the trace ID as the correlation ID.** Then your logs and traces are joined for free: find a slow trace, query logs by that trace ID, get the exact lines.

**How it propagates:** the gateway generates it if absent, every service reads it from the header and puts it in a request-scoped context, and the logger reads from that context automatically. **If developers have to remember to pass it, it will be missing exactly where you need it.** In Go that's `context.Context`; in Node it's `AsyncLocalStorage`.

**The IDs worth carrying on every line:** `trace_id` (this request), `retailer_id` (whose request), `order_id` or `saga_id` (what it's about), `service` and `version` (where from, and which deploy).

That last one matters more than people expect — `version` is what lets you ask "are these errors only on the new deploy?", which is usually the first question during an incident.

### Levels, volume and cost

**Logs are the most expensive pillar** because volume scales linearly with traffic and they're stored verbatim. At scale, ingestion costs real money.

- **ERROR** — something broke and needs attention. Should be rare enough that you could read them all.
- **WARN** — recovered, but notable. A retry succeeded; a circuit breaker opened.
- **INFO** — business events worth keeping. Order placed, payment confirmed. **Deliberate and low-volume.**
- **DEBUG** — off in production by default, ideally toggleable per service or per request without a deploy.

**The practical discipline:** don't log inside a loop over line items. Log once per request with a summary. One high-volume `INFO` in a hot path can be most of your logging bill.

**And: a log line is not a metric.** Counting log lines to derive a rate is expensive and fragile. If you want a number over time, emit a metric.

### Logging in an async world

Two specific problems:

**Ordering.** Log timestamps across machines are not reliably ordered — clock skew of a few hundred milliseconds will scramble the apparent sequence. **Don't reconstruct causality from timestamps; use the trace's span hierarchy**, which has real parent-child relationships.

**Context loss across queues.** A worker processing a job has no idea which request created it, unless you put the trace ID in the message and the worker restores it when processing. **This is the single most common gap in distributed logging** — everything is traceable right up to the queue, then the trail dies.

### PII — the rule that bites people

**Never log phone numbers, addresses, or full payment details.** For this product, the phone number is both PII and the primary identifier, so the temptation to log it is constant.

**Log the retailer ID, not the phone number.** If you need to find a retailer's requests, look up their ID first. Logs are widely readable inside a company, retained for months, and shipped to third-party systems — that's a lot of surface for personal data.

| Pros of centralised structured logging | Cons |
|---|---|
| One query answers "what happened to this request" | Most expensive observability pillar by far |
| Arbitrary fields queryable after the fact | Easy to leak PII |
| Keeps the detail traces and metrics drop | Volume grows with traffic, so cost grows with success |
| Works when tracing is unsampled | Useless without correlation IDs |

**Interview line:** *"Structured JSON with a correlation ID — the trace ID — carried through a request-scoped context so developers can't forget it, and into queue messages so the trail survives async boundaries. Logs carry the retailer ID, never the phone number. And I'd keep INFO deliberately low-volume, because at scale logging cost scales with traffic and one chatty line in a hot path is most of the bill."*


## 83. Inventory and stock correctness · T1

**Why this gets drilled.** It's the cleanest test of whether you understand concurrency. The naive version is obviously wrong once pointed out, and whether you reach for the right fix *immediately* tells an interviewer a lot.

### The race, stated precisely

```
stock = SELECT available FROM inventory WHERE sku_id = 1   -- reads 5
if stock >= 5:                                              -- passes
    UPDATE inventory SET available = available - 5 ...      -- writes 0
```

Two retailers run this at the same moment. Both read 5. Both pass the check. Both subtract 5. **Stock is now -5 and you've sold product you don't have.** The window between the read and the write is where the bug lives — this is a **time-of-check to time-of-use (TOCTOU)** race, and saying that term shows you recognise the class, not just the instance.

### The three correct fixes, and when each applies

**1. Conditional update (the default).**

```sql
UPDATE inventory
SET available = available - :qty
WHERE sku_id = :id AND available >= :qty
```

Affects **one row or zero**. Zero means insufficient stock. No window, because check and write are one statement and the database holds a row lock for its duration. **Cheapest and correct — reach for this first.**

**2. `SELECT ... FOR UPDATE`.** Lock the row, do other work, then write. Use when you need to read the current value and make a decision involving other data before writing. Slightly more expensive and holds the lock longer, so the transaction must stay short.

**3. A database constraint as the backstop.** `CHECK (available >= 0)`. This doesn't *prevent* the race elegantly — it turns a silent corruption into a loud error. **Add it anyway**, because it's the thing that catches the code path someone writes next year that forgot the conditional update. Defence in depth: the constraint is your guarantee, the conditional update is your good behaviour.

**What loses the point:** proposing an application-level lock, a Redis lock, or "we'd use a transaction" without saying what's inside it. A Redis lock for this is wrong — see #49, a lock can expire while the holder thinks it still holds it. **The database constraint is what guarantees stock never goes negative; everything else is optimisation.**

### Reserve vs decrement — the lifecycle

Decrementing at "add to cart" means abandoned carts hold stock forever. Decrementing at delivery means you oversell constantly. So:

| Moment | What happens to stock |
|---|---|
| Add to cart | Nothing |
| Place order | **Reserve** — `reserved += qty`, with an expiry |
| Payment / credit confirmed | Convert reservation to committed |
| Goods dispatched | `on_hand -= qty`, reservation cleared |
| Reservation expires or payment fails | `reserved -= qty`, released |

So **`available = on_hand - reserved`**.

**The reservation expiry is a business decision you should ask about, not assume.** Thirty minutes is reasonable for a card payment. For a B2B credit order approved instantly, you might commit immediately. For an order awaiting distributor confirmation, hours.

**The failure mode to name:** if the sweeper job that releases expired reservations dies, stock stays locked and nobody notices — availability silently drops and you lose sales with no error anywhere. **That job needs a metric and an alert on reservations older than their expiry.** This is a good "what breaks that nobody sees" answer.

### Stock movements as an append-only log

Don't just keep a mutable `available` number. Keep an append-only **stock movement** table: `sku_id, distributor_id, delta, reason (received/reserved/released/sold/returned/damaged/adjusted), reference (order_id), created_at`.

**Why:** the current count becomes derivable and therefore auditable. When the number is wrong — and in physical inventory it will be — you can replay the movements and find exactly which one was wrong. A bare mutable counter gives you a wrong number and no way to explain it.

**Same shape as the ledger in #84**, and that's the pattern worth naming: **for anything where "how did we get here" matters, keep the events and derive the balance.** Cache the current count for speed if you need to, but the movements are the truth.

### Multi-location: the thing B2B adds

Stock isn't one number — it's per SKU **per distributor**, and which distributors can serve a given retailer depends on geography. So "is this available?" is really "is this available from someone who delivers to this pincode?"

That makes availability a **join between inventory and serviceability**, not a column lookup — which is exactly why you denormalise it into a read model per region (#23, #3.5 in the round-2 doc).

**The follow-up:** if two distributors can serve a retailer and both have stock, which one gets the order? Cheapest, fastest, highest fill-rate history, or load-balanced to keep both engaged? **That's a business rule, and saying "that's a business decision, here are the options" is the right answer.**

### Approximate for display, exact for commitment

**Never cache the number you commit against.** Cache "In stock" or "Low stock" for browsing — that's fine and saves enormous read load. But the quantity checked inside the order transaction reads the source of truth.

Say this distinction explicitly. It's the single clearest signal in this topic that you understand where consistency is negotiable and where it isn't.

### The hot SKU problem

If one SKU is wildly popular, every order contends on one row and everything serialises behind it. Throughput collapses to one update at a time.

**The fix** is splitting that SKU's stock into N buckets, each a separate row updated independently, with requests picking one at random. **The cost:** you can report "sold out" while another bucket still has units, because you only checked one.

**The judgement answer:** *"I wouldn't build that yet. At one order a second, row-level contention isn't a problem — and the arithmetic is worth doing out loud before reaching for it. If one SKU became a genuine bottleneck, bucketing is the mechanism, and the cost is slightly pessimistic sold-out reporting."*

### Physical reconciliation

Your database says 40 cases. The warehouse has 37. Breakage, theft, miscounts, goods received but not entered. **Digital inventory always drifts from physical inventory.**

So the system needs: periodic cycle counts, an **adjustment** movement type that records a correction *with a reason* rather than silently overwriting, and a discrepancy report. **Mentioning this unprompted shows you've thought about physical goods rather than just rows**, which is the whole difference between commerce and a CRUD app.

| Pros of reservations + movement log         | Cons                                             |
| ------------------------------------------- | ------------------------------------------------ |
| No overselling; no permanently locked stock | More states and a sweeper job to run and monitor |
| Fully auditable — you can explain any count | More writes per order                            |
| Honest availability shown to other buyers   | Expiry window is a business decision to defend   |
| Physical drift is visible and correctable   | Derived counts need caching for read performance |

**Interview line:** *"Conditional update so the database arbitrates, a `CHECK (available >= 0)` constraint as the backstop for the code path someone writes next year, reservations with an expiry so carts don't lock stock forever, and an append-only movement log so the count is derivable and auditable. Browsing reads an approximate cached value; the order transaction reads the truth."*

## 84. Payments, ledger and money movement · T1

**This is your resume.** Lead with the fact that you built it at Kazam, then go deep.

### Representing money

**Integer minor units — paise — or `NUMERIC`. Never floating point.** 0.1 cannot be represented exactly in binary floating point. In a ledger those tiny errors accumulate until a reconciliation breaks by ₹0.03 and someone spends two days finding it.

**Also store the currency**, even in a single-currency product. It costs one column now and saves a migration later.

### The payment state machine

Payments are not a boolean. Draw this from memory:

```
created → authorized → captured → settled
   ↓          ↓           ↓          ↓
 failed   voided      refunded   disputed
                          ↑
                   partially_refunded
```

**Transitions are validated and mostly one-directional.** A late webhook trying to move a `captured` payment back to `authorized` is **rejected, not applied.** That one rule handles out-of-order delivery, and saying it is the clearest way to show you understand async webhooks.

**Authorise vs capture matters:** authorisation reserves the money without taking it; capture takes it. In commerce you authorise at order placement and capture at dispatch, so you don't hold money for an order you can't fulfil.

### Double-entry, with actual entries

Every transaction produces **at least two entries, and they sum to zero.** The balance of any account is the sum of its entries — never a mutable column.

Retailer pays ₹10,000 for an order:

| Account | Debit | Credit |
|---|---|---|
| Retailer receivable | | 10,000 |
| Cash / gateway clearing | 10,000 | |

Platform commission of ₹500 on that order:

| Account | Debit | Credit |
|---|---|---|
| Distributor payable | 500 | |
| Platform revenue | | 500 |

**Why this is non-negotiable:** the entries sum to zero, so **"do all accounts balance?" is a query you can run continuously.** If it ever returns non-zero, you have a bug and you know it within minutes instead of at the quarterly audit. A mutable `balance` column gives you no such check.

**The rule that follows: never update a posted entry.** To correct something, post a reversing entry. The original stays. **History is immutable; corrections are additions.** This is the same principle as the stock movement log in #83 and the append-only returns in commerce generally.

### Idempotency on money — the highest-stakes case

Everything in #48 applies, but the cost of getting it wrong is charging someone twice.

- **Client-generated key per payment intent**, same key on every retry.
- **Unique constraint in the database** decides the winner — `INSERT ... ON CONFLICT DO NOTHING`. Never check-then-insert.
- **Pass an idempotency key to the gateway too.** Stripe, Razorpay and the rest all support one. Your retry to *them* must also be deduplicated, or you've solved it on your side and still double-charged.
- **Return the stored original response** on a duplicate, not a re-execution.

**Two-sided idempotency is the detail worth volunteering:** your API is idempotent to your clients, *and* your calls to the gateway are idempotent to them. Most candidates only mention the first half.

### Webhooks from the gateway

You built this. The checklist:

- **Verify the HMAC signature** over the raw body, constant-time comparison. Without it, anyone can POST you "payment succeeded."
- **Timestamp inside the signed payload** with a tolerance window, so a captured request can't be replayed later.
- **Deduplicate on the provider's event ID.** They will send duplicates, by design.
- **Expect out-of-order.** `captured` can arrive before `authorized`. The state machine's legal-transition rule handles it: apply the later state, reject the earlier one as an illegal backwards move.
- **Acknowledge fast, process async.** Doing real work inside the handler means the gateway times out and retries, multiplying your load exactly when you're slow.
- **Never trust the webhook body alone for high-value actions.** The safest pattern is to treat the webhook as a *signal* and then call the gateway's API to fetch the authoritative state.

### Reconciliation — how you earn the right to say "no money lost"

Every day, pull the provider's settlement file and compare it to your ledger. Bucket every line:

| Bucket                 | Meaning                        | Action                                               |
| ---------------------- | ------------------------------ | ---------------------------------------------------- |
| **Matched**            | Both sides agree               | Nothing                                              |
| **Missing internally** | They have it, you don't        | Investigate — a webhook you never processed          |
| **Missing externally** | You have it, they don't        | Usually timing; escalate if it persists              |
| **Amount mismatch**    | Both have it, different values | Always investigate — fees, partial capture, or a bug |
| **Status mismatch**    | Different states               | Usually a webhook you missed                         |

**Timing differences clear themselves on the next run.** Real breaks go to a human with enough context to act. Track the **age** of unresolved breaks, not just the count — a break that's been open four days is a different problem from one opened this morning.

**This is the answer to "you claim zero data loss — defend it."** The honest defence is never "my code was correct." It is: *"I had an independent check. The reconciliation job compared our ledger to the provider's settlement file daily, ledger invariants were asserted continuously, and any drift alerted. I know we didn't lose transactions because something other than the happy path was checking."*

### Refunds and reversals

- **Never mutate the original payment.** Create a refund record referencing it, and post reversing ledger entries.
- **Partial refunds** mean a payment can have many refunds; the sum must never exceed the captured amount. **That's a constraint, not a code comment.**
- **A refund can fail.** It's a payment in its own right with its own state machine, not a flag on the original.
- **In a credit-based B2B system, most "refunds" aren't money moving at all** — they're credit notes reducing what the retailer owes. Know which one you're doing; they have completely different accounting.

### Settlement and payouts

Money in from retailers and money out to distributors are separate flows on different schedules. You hold funds in between, net off commissions and adjustments, and pay out in batches.

**The hard parts to name:** a payout batch that partially fails (some distributors paid, some not) is a saga needing per-distributor idempotency; and holding other people's money has regulatory implications — in India that touches RBI rules on payment aggregation, which is a reason to use a licensed provider's escrow rather than holding balances yourself.

**Saying "I'd want the money to sit with a licensed partner rather than on our balance sheet" is a maturity signal**, because it shows you know where the engineering problem becomes a regulatory one.

### Keeping PCI scope small

Don't touch card numbers. Use the gateway's hosted fields or SDK so card data goes from the user's device straight to the provider, and you only ever store a **token**. This keeps you out of the expensive parts of PCI DSS entirely.

**Interview line:** *"Integer paise, a validated payment state machine where a late webhook can't move a captured payment backwards, double-entry append-only ledger so balances are derived and continuously checkable, idempotency on both sides — my API and my calls to the gateway — and daily reconciliation against their settlement file. That reconciliation is the only reason I'd ever claim we didn't lose a transaction."*

## 85. Credit, limits and exposure · T2

**Why it's separate from payments.** In B2B, most orders are on credit — the retailer takes goods today and pays in 7, 14 or 30 days. **The platform is effectively lending**, and that changes what the backend has to do.

### Available credit is a race, exactly like inventory

`available_credit = credit_limit - outstanding - pending_orders`

Two orders placed at the same moment can both pass a limit they jointly exceed. **Same bug, same fix:** a conditional update, not a read-then-check-then-write.

```sql
UPDATE retailer_credit
SET reserved = reserved + :amount
WHERE retailer_id = :id
  AND (limit_paise - outstanding - reserved) >= :amount
```

One row or zero. **Recognising that credit and inventory are the same problem is a good thing to say out loud** — it shows you see the pattern rather than memorising cases.

### What the data model needs

- **Credit limit** per retailer, with a history of changes and who approved them.
- **Outstanding** derived from the ledger, not stored as a mutable number.
- **Reserved** for orders placed but not yet invoiced.
- **Aging buckets** — current, 1–30 days overdue, 31–60, 60+. This is the standard view the business will ask for on day one.
- **Repayment history**, which is both an operational record and the input to any risk scoring later.

### The operational pieces

**Dunning** — the reminder schedule before and after a due date. Automated, escalating, and it must stop immediately when payment lands or you've annoyed a paying customer.

**Blocking** — at what overdue threshold does a retailer stop being able to order? **A business rule that must be configurable**, not hardcoded, because it will change and it will need exceptions.

**Exposure limits** beyond the individual: total credit outstanding across a region or a distributor, so one area's defaults can't sink the business.

### The trade-off to name

**More credit means more orders and more revenue, and also more default risk.** Those move together. So "should we raise limits?" is never purely a growth question.

**The engineering contribution** is making the trade-off measurable: default rate by segment, by tenure, by order frequency; limits that grow with demonstrated repayment rather than being set once at onboarding; and the ability to turn exposure down quickly per segment when something goes wrong.

**Interview line:** *"Credit is structurally the same concurrency problem as inventory — a conditional update, because two orders can otherwise both pass a limit they jointly exceed. Outstanding gets derived from the ledger rather than stored, so it can't drift. And the thing I'd build early is the ability to adjust exposure per segment quickly, because the business will need to pull that lever before anyone has time to write a migration."*


---


# Group 12 — Peak events and flash sales

Added after reading the *Flipkart Big Billion Days — System Design Guide* (mission_compile, Medium). **A note on that article before the topics:** it's a solid beginner-level overview that uses mall analogies, and it contains no Flipkart-internal information — it's a generic flash-sale guide with a Flipkart title. Most of what it covers is already in this document. This group holds the genuinely new material, plus one point where I think the article is wrong.

### Where the article's 12 topics live in this document

| Article topic | Covered in | Status |
|---|---|---|
| Auto-scaling servers | #66 | Covered; forecasting added as #87 |
| Load balancers | #2 | Covered more deeply here (L4/L7, algorithms, health checks) |
| Caching | #29, #30, #31, #33 | Covered much more deeply here |
| Database sharding | #19, #20, #21 | Covered more deeply, including why *not* to shard |
| Message queues | #34, #35 | Covered more deeply (ordering, consumer groups, outbox) |
| Rate limiting | #57 | Covered; fair-allocation angle added in #86 |
| Failover zones | #60, #61 | Covered; see #86 for the peak-event framing |
| AI/ML traffic planning | — | **New — #87** |
| Circuit breakers | #54 | Covered; library names added below |
| Inventory locking | #83 | Covered much more deeply — **and I disagree with the article, see #86** |
| Payment gateway resilience | — | **New — #89** |
| Monitoring and fraud detection | #68, #81, #82 for monitoring | **Fraud/bots new — #90** |

**On circuit breaker libraries**, since the article names them and an interviewer might: **Hystrix** (Netflix, now in maintenance mode — don't propose it for new work), **Resilience4j** (the modern JVM choice), **Polly** (.NET), **gobreaker** (Go), **opossum** (Node). Knowing Hystrix is deprecated is a better signal than knowing it exists.

## 86. Flash sale architecture · T1

**What it is.** Designing for an event where traffic goes up 50–100x at a known moment, and a limited quantity of a hot item is wanted by far more people than can get it.

**Why it's the archetypal Indian e-commerce interview question.** Big Billion Days, Great Indian Festival, and in your world a brand running a scheme on a popular SKU. If you interview anywhere in Indian commerce, you will get some version of this.

### The first move: separate the two problems

This is the thing that distinguishes a good answer. **A flash sale is two completely different problems wearing one name:**

1. **A read problem** — everyone loading the sale page at once. Enormous volume, but it's the *same* content for everyone, so it's solvable with caching and a CDN. This part is almost easy.
2. **A write problem** — everyone trying to buy the same limited SKU. All contention lands on one inventory row. **This is the hard half** and no amount of caching helps.

**Say that split out loud first.** Candidates who treat it as one undifferentiated "scale" problem miss that the solutions are unrelated.

### Handling the read side

- **Pre-warm every cache before the sale opens.** The worst possible time for a cold cache is the second traffic peaks. Load the sale page, the product documents and the price lists into cache in advance.
- **Static-ify the landing page.** The sale page should be a CDN-served artefact, not a dynamic render. Push the countdown and the "sold out" state to a tiny separate API call.
- **Jittered TTLs** so keys don't expire together mid-sale (#33).
- **Scheduled scale-up, not reactive** (#66). Reactive autoscaling is always minutes behind, and the spike is over in minutes.
- **Degrade non-essentials**: turn off recommendations, personalised ranking and heavy analytics for the window. **Shedding features deliberately during a peak is a legitimate engineering decision**, and saying you'd plan it in advance scores well.

### Handling the write side: fair allocation of scarce stock

Everyone wants 500 units. 50,000 people are trying. The options:

| Approach                                | How                                                     | Pros                                           | Cons                                                                       |
| --------------------------------------- | ------------------------------------------------------- | ---------------------------------------------- | -------------------------------------------------------------------------- |
| **First come, first served on the row** | Conditional update, losers get "sold out"               | Simple, correct, no new infrastructure         | One row serialises everything; throughput capped                           |
| **Stock bucketing**                     | Split the 500 into 10 rows of 50, pick at random        | 10x the parallelism                            | Can report "sold out" while a bucket has stock                             |
| **Token / queue admission**             | Issue N+buffer tokens, only token holders can check out | Contention moves off the database; predictable | More moving parts; token issuance becomes the hot path                     |
| **Accept-then-confirm**                 | Take the order as `submitted`, confirm asynchronously   | Fast responses, no contention at peak          | User doesn't know immediately — a **product decision**, not just technical |

**The judgement move: do the arithmetic before choosing.** If you're selling 500 units over ten minutes, that's roughly one write per second, and a single row lock is completely fine. **Most "flash sale" write problems aren't actually write problems** — they're read storms with a small write core. Reaching for bucketing before checking the number is exactly the over-engineering the prioritisation axis is looking for.

### Where I disagree with the article: locking at add-to-cart

The article says to reserve stock when an item enters the cart. **That's right for a flash sale and wrong as a general rule, and knowing the difference is the valuable part.**

- **Flash sale:** reserving at cart makes sense, because the scarce resource is the item and the fair thing is to give the person who got there first a short window to pay. The lock must be **very short** — minutes — or abandoned carts strand all the stock.
- **Normal B2B restocking:** reserving at cart is wrong. A kirana retailer builds a basket of 30 items over several minutes while serving customers. Locking stock for all of it means abandoned baskets freeze inventory that other shops need, and in B2B the basket is large and the browsing is slow.

**Interview line:** *"Reservation timing is a business decision, not a default. For a flash sale I'd reserve at cart with a very short expiry, because fairness to whoever arrived first is the point. For normal B2B ordering I'd reserve at order placement, because retailers build large baskets slowly and locking stock through that would strand inventory other shops need."*

That answer is strictly better than either rule on its own, and it's the kind of thing that demonstrates product sense inside a technical answer.

### Failover during a peak event

The article's "failover zones" matter most here, because **a peak event is exactly when you can least afford to lose a zone.** Multi-AZ with synchronous replication is cheap and should be the default (#61). Multi-region active-active means accepting asynchronous replication and therefore **write conflicts you have to resolve** — which during a flash sale means two regions can both sell the last unit.

**The honest position:** *"For an India-only user base, multi-region buys disaster recovery, not latency, and active-active writes would reintroduce the overselling problem I just spent effort eliminating. I'd run multi-AZ, keep cross-region backups for DR, and accept a regional outage as a rare total outage rather than take on conflict resolution on inventory."*

### The pre-event checklist worth reciting

This is a strong closing move if a flash-sale question comes up, because it shows you've thought operationally and not just architecturally:

1. Load test at expected peak **against production-scale data** (#67).
2. Pre-warm caches and pre-scale instances on a schedule.
3. Raise database connection limits and check PgBouncer sizing (#7, #3.7).
4. Feature-flag off everything non-essential so you can shed fast (#64).
5. Freeze deploys for the window.
6. Pre-agree the degradation plan: what gets turned off first, and who decides.
7. Have a war room with the business metric on screen — **orders per minute, not CPU** (#68).
8. Plan the ramp-down too; traffic falling off a cliff causes its own problems with scaled-up infrastructure and cold caches.

**Interview line:** *"I'd split it into the read storm and the write contention, because they have unrelated solutions. The read side is pre-warmed caches, a CDN-served static landing page and scheduled scale-up. The write side I'd size first — often it's only a few writes a second and one row is fine. And I'd plan the degradation list in advance, because deciding what to turn off at peak is not a decision you want to make at peak."*

## 87. Predictive scaling and demand forecasting · T2

**What it is.** Scaling *before* the load arrives, using history and known events, instead of reacting to a metric.

**Why reactive autoscaling fails at peaks.** An instance takes one to three minutes to start, register with the load balancer and warm up. A flash sale spike arrives in seconds. **By the time reactive scaling responds, the event is over and your users already saw errors.**

**The three approaches, in increasing order of effort:**

1. **Scheduled scaling.** You know the sale starts at 8pm; scale up at 7pm. Boring, trivially reliable, and it covers most of the value. **Start here.**
2. **Historical pattern scaling.** Learn the daily and weekly shape — kirana retailers order in the morning before the shop gets busy, and on particular weekdays — and pre-scale to the curve.
3. **Predictive / ML forecasting.** Forecast from historical load, marketing calendar, seasonality and real-time leading indicators.

**The honest take to give:** *"Scheduled scaling for known events plus reactive scaling as the safety net gets you most of the benefit for almost none of the complexity. I'd only build forecasting if we had frequent unpredictable spikes we couldn't anticipate, and even then I'd keep a generous reactive floor underneath it — a forecast that's wrong in the low direction is worse than no forecast, because you've convinced yourself you're covered."*

| Pros                                             | Cons                                                                 |
| ------------------------------------------------ | -------------------------------------------------------------------- |
| Capacity is there before the load arrives        | A wrong prediction leaves you worse off than reactive                |
| Smooths cost — scale down confidently off-peak   | Needs clean historical data                                          |
| Avoids the cold-start cliff for caches and pools | ML forecasting is a lot of machinery for a cron job's worth of value |

**The cost lever the article raises and is worth knowing:** **spot instances** for stateless, interruptible capacity (batch workers, async consumers) at a large discount, with on-demand for the request path. Never put stateful or latency-critical work on spot.

**Interview line:** *"Scheduled scaling for known events, reactive as the backstop. Reactive alone can't catch a spike that arrives faster than an instance boots — which is every flash sale."*

## 88. Virtual waiting rooms and admission control · T2

**What it is.** When demand exceeds capacity, let a controlled number of users through and hold the rest in a queue with a visible position, instead of letting everyone in and failing everyone.

**The insight:** a system at 300% of capacity serves **nobody** — every request times out, everyone retries, and the retries make it worse. A system that admits 100% and queues 200% serves everyone, just not simultaneously. **Honest queueing beats dishonest failure.**

**How it works:** the user hits the sale page and gets a queue token. A gatekeeper (usually at the edge, often a Redis sorted set keyed by arrival time) admits N users per second as capacity frees up. The waiting page shows position and estimated wait — and **showing position matters**, because a visible queue stops people from refreshing, and refresh storms are what kill you.

| Pros                                                 | Cons                                             |
| ---------------------------------------------------- | ------------------------------------------------ |
| The system stays within capacity, so it stays up     | Users wait, which is a product cost              |
| Users get a fair, visible ordering                   | Real implementation complexity                   |
| Stops the refresh storm that compounds overload      | The gatekeeper itself must survive the full load |
| Lets you plan capacity around a known admission rate | Feels unfair if the queue isn't actually ordered |

**The related, simpler mechanism — load shedding (#56)** — is the same principle without the user experience: reject with `429` and `Retry-After` rather than accepting work you can't do.

**For Kirana Club specifically:** a full waiting room is almost certainly over-engineering. The useful half is **admission control at the edge** — a cap on concurrent checkout operations so the order path never gets more than it can handle, with clean `429`s for the overflow.

**Interview line:** *"A waiting room is honest queueing instead of dishonest failure — at 300% of capacity everyone gets errors, so admitting 100% and queueing the rest serves more people. For this product I'd start with admission control and proper 429s rather than a full waiting room, which is a lot of machinery for a problem we may not have."*

## 89. Payment gateway resilience and multi-gateway routing · T1

**Why this matters and is often missed.** Your payment gateway *will* have an outage, and in India this is a regular occurrence — a bank's UPI endpoint degrades, a gateway has a bad hour. **If you have one gateway, their outage is your outage, and it hits revenue directly.**

### Multi-gateway routing

Integrate two or more providers behind **one internal payment abstraction**, so the rest of your system never knows which one handled a transaction.

**Routing rules you can apply:** route by method (one provider better at UPI, another at cards); route by cost, since rates differ per method and volume; route by live success rate, shifting traffic away from a degrading provider; and **failover on a circuit breaker opening** (#54).

**The hard parts, and naming them is the signal:**

- **Reconciliation gets multiplied.** Each gateway has its own settlement file, format and schedule. **Your reconciliation job (#84) becomes one per provider**, and your ledger needs to record which provider handled each transaction.
- **Refunds must go back through the original provider.** You cannot refund a Razorpay charge via PayU. So the provider identity is permanent on the transaction, not a routing decision you can re-make.
- **Idempotency keys are per provider.** Your key namespace has to be scoped, or a retry that gets routed to a different provider isn't deduplicated at all.
- **Testing doubles.** Every change needs validating against every provider's sandbox.

**The judgement line:** *"Multi-gateway is real resilience and real ongoing cost — double the reconciliation, double the integration surface. I'd start with one provider plus a clean abstraction boundary, so adding a second is a week's work rather than a rewrite, and add it when gateway downtime actually costs us measurable revenue. That's a number I'd want before paying the complexity."*

### Pending is a state, not a failure

**The most important single idea in this topic.** When a payment call times out, you do not know whether it succeeded (#44, #53). So the order does **not** go to `failed`. It goes to **`payment_pending`**, and a reconciliation job resolves it by querying the gateway's API for the authoritative status.

**If you mark it failed and the charge actually went through, you've taken the retailer's money and given them nothing** — and they will find out before you do. This is the exact ghost-transaction class you eliminated at Kazam, so say so.

### Other resilience pieces

- **Idempotency keys on every call to the gateway**, so your retry doesn't double-charge (#84).
- **Timeouts shorter than the user's patience**, with the pending state as the fallback.
- **Asynchronous confirmation** — accept the order, confirm payment out of band, notify the retailer. This is especially right for a B2B credit flow where the payment isn't instant anyway.
- **A status-polling fallback** for when webhooks don't arrive. Never rely on webhooks as your only source of truth; they're a latency optimisation over polling, not a guarantee.

| Pros of multi-gateway | Cons |
|---|---|
| One provider's outage stops being your outage | Reconciliation work multiplies per provider |
| Route by cost and by success rate | More integration surface to test and maintain |
| Negotiating leverage with providers | Refunds are locked to the original provider |
| Method-specific strengths exploited | Idempotency and ledger both need provider scoping |

**Interview line:** *"The single most important thing is that a payment timeout means 'pending', never 'failed' — you can't tell a lost response from a failed charge, so you resolve it by querying the gateway, not by guessing. That's the ghost-transaction problem I dealt with at Kazam. Multi-gateway routing on top of that is worth it once gateway downtime costs measurable revenue, and the hidden cost is that reconciliation multiplies per provider."*

## 90. Bot mitigation and fraud detection · T2

**Why it's a commerce problem specifically.** On a flash sale, bots buy the scarce stock in milliseconds and resell it. In B2B, the concerns shift: **competitors scraping your pricing** (which is genuinely commercially sensitive in a distribution business), fake retailer accounts farming referral or first-order incentives, and **credit fraud** — a retailer who onboards, maxes their credit limit and vanishes.

### Layered defences, cheapest first

1. **Rate limiting** (#57) by account and by IP. Stops the crude cases.
2. **Device fingerprinting** — browser and device signals identifying one actor across many accounts. Catches the person running 50 fake retailer accounts from one phone.
3. **CAPTCHA**, but **only on suspicion**, never by default. For a retailer on a low-end phone over 3G, a CAPTCHA is a wall. **Say this** — a friction control that blocks your legitimate users is a product failure, and it's the kind of trade-off this JD is screening for.
4. **Behavioural signals** — purchase velocity far beyond what a shop could sell, adding to cart in 200ms, ordering patterns with no human rhythm.
5. **Anomaly detection on business metrics** — one account placing 100x the normal order volume, or a new account immediately drawing full credit.

### The architectural point worth making

**Fraud checks belong asynchronously beside the order path, not inside it.** A synchronous fraud API in the order transaction means a fraud-service outage stops all orders. **Score asynchronously, flag for review, and hold fulfilment rather than blocking order creation** — you can always cancel before dispatch, and the pivot transaction (#47) is exactly the point before which cancelling is cheap.

**That's a genuinely good answer** because it connects fraud handling to the saga pivot: you have a free window between order and dispatch in which to be suspicious.

### The trade-off to state

**Every fraud control has a false positive rate, and a false positive is a real customer you turned away.** For a kirana retailer placing their first order, being blocked is likely the end of that relationship — they go back to their old distributor.

**So the framing is:** *"I'd tune for low false positives and accept some fraud, because at this stage of the business the cost of losing a genuine retailer is higher than the cost of a fraudulent order. That ratio changes as we grow, and the system should make the threshold a configuration rather than a code change."*

| Pros | Cons |
|---|---|
| Protects scarce stock, margins and credit exposure | Every control has false positives — real customers blocked |
| Scraping protection guards commercially sensitive pricing | ML approaches need labelled fraud data you may not have |
| Async scoring keeps it off the critical path | An arms race; attackers adapt |
| Credit fraud detection protects real money | Friction controls hit your worst-connected users hardest |

**Interview line:** *"Layered, cheapest first — rate limits, then device fingerprinting, then behavioural signals, with CAPTCHA only on suspicion because it's a wall for a retailer on a low-end phone. And fraud scoring runs asynchronously beside the order path rather than inside it, so a fraud-service outage can't stop orders and we still have the window before dispatch to cancel."*

---