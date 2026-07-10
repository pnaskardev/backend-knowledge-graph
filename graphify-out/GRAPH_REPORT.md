# Graph Report - .  (2026-07-10)

## Corpus Check
- 317 files · ~90,381 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 395 nodes · 909 edges · 33 communities (25 shown, 8 thin omitted)
- Extraction: 96% EXTRACTED · 4% INFERRED · 0% AMBIGUOUS · INFERRED: 34 edges (avg confidence: 0.74)
- Token cost: 0 input · 893,670 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Caching & CAP Trade-offs|Caching & CAP Trade-offs]]
- [[_COMMUNITY_Kafka Streaming & Feeds|Kafka Streaming & Feeds]]
- [[_COMMUNITY_Saga Orchestration Flow|Saga Orchestration Flow]]
- [[_COMMUNITY_Kubernetes Workloads|Kubernetes Workloads]]
- [[_COMMUNITY_Microservices Reliability Patterns|Microservices Reliability Patterns]]
- [[_COMMUNITY_Architecture Pattern Index|Architecture Pattern Index]]
- [[_COMMUNITY_Relational Databases & Indexing|Relational Databases & Indexing]]
- [[_COMMUNITY_Distributed Data & Replication|Distributed Data & Replication]]
- [[_COMMUNITY_Low-Level Design Problems|Low-Level Design Problems]]
- [[_COMMUNITY_Event Messaging Diagrams|Event Messaging Diagrams]]
- [[_COMMUNITY_Message Queue Fundamentals|Message Queue Fundamentals]]
- [[_COMMUNITY_Consistency & CAP Theory|Consistency & CAP Theory]]
- [[_COMMUNITY_Distributed Cache Internals|Distributed Cache Internals]]
- [[_COMMUNITY_Event-Driven Architecture|Event-Driven Architecture]]
- [[_COMMUNITY_Transactions & Concurrency|Transactions & Concurrency]]
- [[_COMMUNITY_RabbitMQ Exchange Routing|RabbitMQ Exchange Routing]]
- [[_COMMUNITY_Resilience & Retry Patterns|Resilience & Retry Patterns]]
- [[_COMMUNITY_Delivery Semantics & Idempotency|Delivery Semantics & Idempotency]]
- [[_COMMUNITY_OOP Design Patterns|OOP Design Patterns]]
- [[_COMMUNITY_K8s Deployment & Scaling|K8s Deployment & Scaling]]
- [[_COMMUNITY_Obsidian App Config|Obsidian App Config]]
- [[_COMMUNITY_Obsidian App Config (dup)|Obsidian App Config (dup)]]
- [[_COMMUNITY_Gateway & Service Routing|Gateway & Service Routing]]
- [[_COMMUNITY_Containerization|Containerization]]
- [[_COMMUNITY_Dead Letter Handling|Dead Letter Handling]]
- [[_COMMUNITY_Database Index Types|Database Index Types]]
- [[_COMMUNITY_Food Delivery (LLD)|Food Delivery (LLD)]]
- [[_COMMUNITY_Logger (LLD)|Logger (LLD)]]
- [[_COMMUNITY_Vault Overview|Vault Overview]]
- [[_COMMUNITY_Concept Template|Concept Template]]
- [[_COMMUNITY_Vault Overview (dup)|Vault Overview (dup)]]
- [[_COMMUNITY_Pattern Template|Pattern Template]]
- [[_COMMUNITY_System Design Template|System Design Template]]

## God Nodes (most connected - your core abstractions)
1. `Messaging MOC` - 33 edges
2. `Sharding` - 28 edges
3. `Microservices MOC` - 24 edges
4. `Distributed Cache` - 22 edges
5. `Databases MOC` - 22 edges
6. `Distributed Systems MOC` - 22 edges
7. `Idempotency` - 20 edges
8. `Microservices MOC` - 19 edges
9. `Backend Engineering Knowledge Map (Home)` - 19 edges
10. `Backend Engineering Knowledge Map (Home)` - 18 edges

## Surprising Connections (you probably didn't know these)
- `Cache (LLD)` --semantically_similar_to--> `Distributed Cache (System Design)`  [INFERRED] [semantically similar]
  💻 LLD Problems/Cache (LLD).md → 🏛️ System Designs/Distributed Cache (System Design).md
- `Covering Index` --semantically_similar_to--> `Clustered Index`  [INFERRED] [semantically similar]
  📝 Concepts/Covering Index.md → backend-knowledge-vault/vault/📝 Concepts/Clustered Index.md
- `Backpressure` --semantically_similar_to--> `Circuit Breaking Concepts`  [INFERRED] [semantically similar]
  backend-knowledge-vault/vault/📝 Concepts/Message Queue.md → backend-knowledge-vault/vault/📝 Concepts/Circuit Breaking Concepts.md
- `Rate Limiter` --references--> `Backpressure`  [EXTRACTED]
  🏛️ System Designs/Rate Limiter.md → backend-knowledge-vault/vault/📝 Concepts/Message Queue.md
- `Cache (LLD)` --references--> `Cache Aside`  [EXTRACTED]
  💻 LLD Problems/Cache (LLD).md → backend-knowledge-vault/vault/📝 Concepts/Cache Aside.md

## Import Cycles
- None detected.

## Hyperedges (group relationships)
- **Payment gateway exactly-once reliability stack** — backend_knowledge_vault_vault_system_designs_payment_gateway_payment_gateway, backend_knowledge_vault_vault_concepts_idempotency_idempotency, backend_knowledge_vault_vault_patterns_saga_pattern_saga_pattern, backend_knowledge_vault_vault_patterns_transactional_outbox_transactional_outbox [INFERRED 0.75]
- **Reliable async notification delivery** — backend_knowledge_vault_vault_system_designs_notification_service_notification_service, backend_knowledge_vault_vault_concepts_message_queue_message_queue, backend_knowledge_vault_vault_concepts_retry_strategies_retry_strategies, backend_knowledge_vault_vault_concepts_dead_letter_queue_dead_letter_queue [INFERRED 0.75]
- **Distributed cache resilience** — backend_knowledge_vault_vault_system_designs_distributed_cache_system_design_distributed_cache_system_design, backend_knowledge_vault_vault_concepts_cache_stampede_cache_stampede, backend_knowledge_vault_vault_concepts_cache_avalanche_cache_avalanche, backend_knowledge_vault_vault_concepts_quorum_reads_and_writes_quorum_reads_and_writes [INFERRED 0.75]
- **Caching failure modes** — backend_knowledge_vault_vault_concepts_cache_stampede_cache_stampede, backend_knowledge_vault_vault_concepts_cache_avalanche_cache_avalanche, backend_knowledge_vault_vault_concepts_cache_penetration_cache_penetration [INFERRED 0.75]
- **Consensus-based coordination** — backend_knowledge_vault_vault_concepts_consensus_algorithms_consensus_algorithms, concepts_leader_election_leader_election, concepts_distributed_locking_distributed_locking, concepts_split_brain_split_brain [INFERRED 0.75]
- **Kafka consumption flow** — backend_knowledge_vault_vault_concepts_consumer_consumer, backend_knowledge_vault_vault_concepts_consumer_groups_consumer_groups, concepts_partition_partition, concepts_offset_offset [INFERRED 0.75]
- **RabbitMQ Exchange Routing Types** — backend_knowledge_vault_backend_knowledge_vault_vault_concepts_exchange_exchange, backend_knowledge_vault_backend_knowledge_vault_vault_concepts_direct_exchange_direct_exchange, backend_knowledge_vault_backend_knowledge_vault_vault_concepts_fanout_exchange_fanout_exchange, backend_knowledge_vault_backend_knowledge_vault_vault_concepts_headers_exchange_headers_exchange [INFERRED 0.85]
- **Retry Resilience with Backoff and Jitter** — backend_knowledge_vault_backend_knowledge_vault_vault_concepts_retry_strategies_retry_strategies, backend_knowledge_vault_backend_knowledge_vault_vault_concepts_exponential_backoff_exponential_backoff, backend_knowledge_vault_backend_knowledge_vault_vault_concepts_jitter_jitter [INFERRED 0.85]
- **Reliable Message Delivery Semantics** — backend_knowledge_vault_backend_knowledge_vault_vault_concepts_exactly_once_vs_at_least_once_vs_at_most_once_exactly_once_vs_at_least_once_vs_at_most_once, backend_knowledge_vault_backend_knowledge_vault_vault_concepts_idempotency_idempotency, backend_knowledge_vault_backend_knowledge_vault_vault_concepts_inbox_pattern_inbox_pattern [INFERRED 0.75]
- **Kafka message flow** — backend_knowledge_vault_vault_concepts_producer_producer, backend_knowledge_vault_vault_concepts_topic_topic, backend_knowledge_vault_vault_concepts_partition_partition, backend_knowledge_vault_vault_concepts_offset_offset, backend_knowledge_vault_vault_concepts_consumer_consumer [INFERRED 0.75]
- **RabbitMQ routing flow** — backend_knowledge_vault_vault_concepts_exchange_exchange, backend_knowledge_vault_vault_concepts_binding_binding, backend_knowledge_vault_vault_concepts_routing_key_routing_key, backend_knowledge_vault_vault_concepts_queue_queue [INFERRED 0.75]
- **Kubernetes pod health probes** — backend_knowledge_vault_vault_concepts_pod_pod, backend_knowledge_vault_vault_concepts_liveness_probe_liveness_probe, backend_knowledge_vault_vault_concepts_readiness_probe_readiness_probe [INFERRED 0.75]
- **Cache write/refresh patterns** — concepts_write_through_write_through, backend_knowledge_vault_vault_concepts_write_behind_write_behind, concepts_refresh_ahead_refresh_ahead [INFERRED 0.85]
- **Retry reliability mechanisms** — concepts_retry_strategies_retry_strategies, concepts_exponential_backoff_exponential_backoff, concepts_jitter_jitter, backend_knowledge_vault_vault_concepts_circuit_breaking_concepts_circuit_breaking_concepts [EXTRACTED 1.00]
- **Database scaling techniques** — concepts_replication_replication, backend_knowledge_vault_vault_concepts_sharding_sharding, concepts_partitioning_partitioning [EXTRACTED 1.00]
- **Resilience Patterns** — backend_knowledge_vault_vault_patterns_circuit_breaker, backend_knowledge_vault_vault_patterns_retry_pattern, backend_knowledge_vault_vault_patterns_timeout_pattern, backend_knowledge_vault_vault_patterns_bulkhead_pattern, backend_knowledge_vault_vault_patterns_fallback_pattern [INFERRED 0.85]
- **Sidecar Deployment Patterns** — backend_knowledge_vault_vault_patterns_sidecar_pattern, backend_knowledge_vault_vault_patterns_ambassador_pattern, backend_knowledge_vault_vault_patterns_adapter_pattern_deployment [INFERRED 0.85]
- **Event-Driven Data Consistency** — backend_knowledge_vault_vault_patterns_saga_pattern, backend_knowledge_vault_vault_patterns_cqrs, backend_knowledge_vault_vault_patterns_event_driven_architectures, backend_knowledge_vault_vault_patterns_inbox_pattern, backend_knowledge_vault_vault_patterns_database_per_service [INFERRED 0.75]
- **Payment gateway exactly-once consistency flow** — system_designs_payment_gateway_payment_gateway, concepts_idempotency_idempotency, patterns_saga_pattern_saga_pattern, backend_knowledge_vault_vault_patterns_transactional_outbox_transactional_outbox, concepts_exactly_once_vs_at_least_once_vs_at_most_once_exactly_once_vs_at_least_once_vs_at_most_once [INFERRED 0.75]
- **Notification reliable async delivery flow** — system_designs_notification_service_notification_service, concepts_message_queue_message_queue, concepts_retry_strategies_retry_strategies, concepts_dead_letter_queue_dead_letter_queue, patterns_event_driven_architectures_event_driven_architectures [INFERRED 0.75]
- **Cache-heavy read-scaling stack** — concepts_distributed_cache_distributed_cache, backend_knowledge_vault_vault_concepts_cache_aside_cache_aside, backend_knowledge_vault_vault_concepts_sharding_sharding [INFERRED 0.65]
- **Cache Failure Modes** — backend_knowledge_vault_vault_concepts_cache_stampede_cache_stampede, backend_knowledge_vault_vault_concepts_cache_avalanche_cache_avalanche, backend_knowledge_vault_vault_concepts_cache_penetration_cache_penetration [INFERRED 0.75]
- **Database Index Types** — backend_knowledge_vault_vault_concepts_clustered_index_clustered_index, backend_knowledge_vault_vault_concepts_composite_index_composite_index, concepts_covering_index_covering_index, concepts_secondary_index_secondary_index [INFERRED 0.75]
- **Distributed Coordination** — backend_knowledge_vault_vault_concepts_consensus_algorithms_consensus_algorithms, concepts_quorum_reads_and_writes_quorum_reads_and_writes, backend_knowledge_vault_vault_concepts_clock_synchronization_clock_synchronization, backend_knowledge_vault_vault_concepts_consistency_models_consistency_models [INFERRED 0.75]
- **RabbitMQ Exchange Routing Family** — concepts_exchange_exchange, concepts_direct_exchange_direct_exchange, concepts_fanout_exchange_fanout_exchange, concepts_headers_exchange_headers_exchange [EXTRACTED 1.00]
- **Retry Backoff Jitter Flow** — concepts_retry_strategies_retry_strategies, concepts_exponential_backoff_exponential_backoff, concepts_jitter_jitter [INFERRED 0.85]
- **Failure Handling Resilience Patterns** — concepts_failure_handling_failure_handling, backend_knowledge_vault_vault_concepts_circuit_breaking_concepts_circuit_breaking_concepts, concepts_bulkhead_pattern_bulkhead_pattern, concepts_timeout_pattern_timeout_pattern [EXTRACTED 1.00]
- **Kafka message flow (producer to consumer via partitions/offsets)** — concepts_producer_producer, concepts_partition_partition, concepts_offset_offset, backend_knowledge_vault_vault_concepts_consumer_consumer, concepts_kafka_kafka [INFERRED 0.75]
- **RabbitMQ routing (exchange to queue via binding/routing key)** — concepts_rabbitmq_rabbitmq, concepts_exchange_exchange, backend_knowledge_vault_vault_concepts_binding_binding, concepts_routing_key_routing_key, concepts_queue_queue [INFERRED 0.75]
- **Kubernetes pod health probes** — concepts_pod_pod, concepts_liveness_probe_liveness_probe, concepts_readiness_probe_readiness_probe [INFERRED 0.75]
- **Retry reliability pattern** — concepts_retry_strategies_retry_strategies, concepts_exponential_backoff_exponential_backoff, concepts_jitter_jitter, backend_knowledge_vault_vault_concepts_circuit_breaking_concepts_circuit_breaking_concepts [INFERRED 0.85]
- **Cache write patterns** — backend_knowledge_vault_vault_concepts_cache_aside_cache_aside, concepts_write_through_write_through, backend_knowledge_vault_vault_concepts_write_behind_write_behind, concepts_refresh_ahead_refresh_ahead [INFERRED 0.85]
- **RabbitMQ exchange routing** — concepts_exchange_exchange, concepts_routing_key_routing_key, backend_knowledge_vault_vault_concepts_topic_exchange_topic_exchange, concepts_direct_exchange_direct_exchange [INFERRED 0.85]
- **Microservice data consistency (Saga) flow** — patterns_saga_pattern_saga_pattern, backend_knowledge_vault_vault_patterns_transactional_outbox_transactional_outbox, patterns_event_driven_architectures_event_driven_architectures, patterns_database_per_service_database_per_service, patterns_cqrs_cqrs [INFERRED 0.85]
- **Microservice resilience pattern toolkit** — patterns_circuit_breaker_circuit_breaker, patterns_retry_pattern_retry_pattern, patterns_timeout_pattern_timeout_pattern, patterns_bulkhead_pattern_bulkhead_pattern, patterns_fallback_pattern_fallback_pattern [INFERRED 0.85]
- **Sidecar deployment pattern family** — patterns_sidecar_pattern_sidecar_pattern, patterns_ambassador_pattern_ambassador_pattern, patterns_adapter_pattern_deployment_adapter_pattern_deployment [INFERRED 0.85]

## Communities (33 total, 8 thin omitted)

### Community 0 - "Caching & CAP Trade-offs"
Cohesion: 0.11
Nodes (52): Cache Aside, Cache Avalanche, Cache Invalidation, Cache Penetration, Cache Stampede, CAP Theorem, Circuit Breaking Concepts, Clock Synchronization (+44 more)

### Community 1 - "Kafka Streaming & Feeds"
Cohesion: 0.11
Nodes (45): Backpressure, Binding, Consumer, Consumer Groups, Kafka, Kafka Replay, Message Ordering, News Feed (+37 more)

### Community 2 - "Saga Orchestration Flow"
Cohesion: 0.11
Nodes (41): API Gateway, Browser, Centralized Decision Making, Choreography, Compensating Transaction, CQRS, createOrder(), Create Order Saga (+33 more)

### Community 3 - "Kubernetes Workloads"
Cohesion: 0.15
Nodes (27): ConfigMap, Container, Deployment, Horizontal Pod Autoscaler, Ingress, Kubernetes, Liveness Probe, Pod (+19 more)

### Community 4 - "Microservices Reliability Patterns"
Cohesion: 0.19
Nodes (26): Transactional Outbox, Exactly Once vs At Least Once vs At Most Once, Idempotency, Inbox Pattern, Payment Gateway, Food Delivery, Microservices MOC, Adapter Pattern (Deployment) (+18 more)

### Community 5 - "Architecture Pattern Index"
Cohesion: 0.16
Nodes (24): How to study fast, Kubernetes MOC, Low Level Design MOC, Messaging MOC, Microservices MOC, System Design MOC, Adapter Pattern (Deployment), Ambassador Pattern (+16 more)

### Community 6 - "Relational Databases & Indexing"
Cohesion: 0.25
Nodes (18): ACID, B+ Trees, BASE, Clustered Index, Composite Index, Databases MOC, Covering Index, Isolation Levels (+10 more)

### Community 7 - "Distributed Data & Replication"
Cohesion: 0.22
Nodes (18): Distributed Cache, Distributed Locking, Leader Election, Partitioning, Quorum Reads and Writes, Read Replicas, Replication, Sharding (+10 more)

### Community 8 - "Low-Level Design Problems"
Cohesion: 0.20
Nodes (18): SOLID Principles, Chess, Elevator, Parking Lot, Splitwise, Chess, Design Patterns, Elevator (+10 more)

### Community 9 - "Event Messaging Diagrams"
Cohesion: 0.27
Nodes (16): Consumer, Event Backbone, Publish/Subscribe Diagram, Event Backbone Diagram, Microservices Application with Event Backbone Diagram, Point-to-Point Messaging Diagram, Point-to-Point Messaging Diagram (2), JSON/HTTP API (+8 more)

### Community 10 - "Message Queue Fundamentals"
Cohesion: 0.19
Nodes (15): Dead Letter Queue, Event Driven Architecture, Exchange, Fanout Exchange, Kafka vs RabbitMQ, Message Queue, Notification Service, Point to Point Messaging (+7 more)

### Community 11 - "Consistency & CAP Theory"
Cohesion: 0.18
Nodes (11): CAP Theorem, Consistency Models, Distributed Systems MOC, Distributed Systems Trade-offs, DynamoDB-style Stores, Isolation Levels, MVCC, Optimistic Locking (+3 more)

### Community 12 - "Distributed Cache Internals"
Cohesion: 0.22
Nodes (9): Cache Invalidation, Cache Stampede, Distributed Cache, Distributed Cache (System Design), Distributed Locking, Leader Election, Redis, Sharding (+1 more)

### Community 13 - "Event-Driven Architecture"
Cohesion: 0.22
Nodes (9): CQRS, Event Driven Architecture, Event-Driven Architectures, Event Versioning, Fanout Exchange, Kafka, Message Queue, Publish Subscribe (+1 more)

### Community 14 - "Transactions & Concurrency"
Cohesion: 0.28
Nodes (9): Exactly Once vs At Least Once vs At Most Once, Isolation Levels, MVCC, Optimistic Locking, Pessimistic Locking, Transactions, ATM, BookMyShow (+1 more)

### Community 15 - "RabbitMQ Exchange Routing"
Cohesion: 0.33
Nodes (7): Binding, Direct Exchange, Exchange, Headers Exchange, RabbitMQ, Routing Key, Topic Exchange

### Community 16 - "Resilience & Retry Patterns"
Cohesion: 0.33
Nodes (7): Bulkhead Pattern, Circuit Breaking Concepts, Exponential Backoff, Failure Handling, Jitter, Retry Strategies, Timeout Pattern

### Community 17 - "Delivery Semantics & Idempotency"
Cohesion: 0.43
Nodes (7): Exactly Once vs At Least Once vs At Most Once, Idempotency, Inbox Pattern, Kafka Replay, Offset, Payment Gateway, SAGA Pattern

### Community 18 - "OOP Design Patterns"
Cohesion: 0.33
Nodes (6): Chess, Design Patterns, Elevator, Logger, Parking Lot, SOLID Principles

### Community 19 - "K8s Deployment & Scaling"
Cohesion: 0.50
Nodes (4): Deployment, Horizontal Pod Autoscaler, Readiness Probe, ReplicaSet

### Community 20 - "Obsidian App Config"
Cohesion: 0.50
Nodes (3): alwaysUpdateLinks, attachmentFolderPath, newLinkFormat

### Community 21 - "Obsidian App Config (dup)"
Cohesion: 0.50
Nodes (3): alwaysUpdateLinks, attachmentFolderPath, newLinkFormat

### Community 22 - "Gateway & Service Routing"
Cohesion: 0.67
Nodes (3): API Gateway, Ingress, Service

### Community 23 - "Containerization"
Cohesion: 0.67
Nodes (3): Container, Docker, Kubernetes

### Community 24 - "Dead Letter Handling"
Cohesion: 0.67
Nodes (3): Dead Letter Queue, Poison Messages, Queue

## Knowledge Gaps
- **82 isolated node(s):** `alwaysUpdateLinks`, `newLinkFormat`, `attachmentFolderPath`, `alwaysUpdateLinks`, `newLinkFormat` (+77 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **8 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Messaging MOC` connect `Kafka Streaming & Feeds` to `Caching & CAP Trade-offs`?**
  _High betweenness centrality (0.068) - this node is a cross-community bridge._
- **Why does `Sharding` connect `Distributed Data & Replication` to `Caching & CAP Trade-offs`, `Kafka Streaming & Feeds`, `Microservices Reliability Patterns`, `Relational Databases & Indexing`?**
  _High betweenness centrality (0.049) - this node is a cross-community bridge._
- **Why does `Kubernetes MOC` connect `Kubernetes Workloads` to `Caching & CAP Trade-offs`?**
  _High betweenness centrality (0.042) - this node is a cross-community bridge._
- **What connects `alwaysUpdateLinks`, `newLinkFormat`, `attachmentFolderPath` to the rest of the system?**
  _82 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Caching & CAP Trade-offs` be split into smaller, more focused modules?**
  _Cohesion score 0.11463046757164404 - nodes in this community are weakly interconnected._
- **Should `Kafka Streaming & Feeds` be split into smaller, more focused modules?**
  _Cohesion score 0.11313131313131314 - nodes in this community are weakly interconnected._
- **Should `Saga Orchestration Flow` be split into smaller, more focused modules?**
  _Cohesion score 0.10853658536585366 - nodes in this community are weakly interconnected._