---
aliases: [Schema Registry, Event Versioning]
---
# Schema Evolution & Event Versioning

> Events outlive the code that wrote them. Versioning is the problem, a schema registry is the tooling.

## Why it matters
<!-- a consumer may read an event written months ago by a producer that has since changed. Replay makes this certain, not hypothetical. -->

## Event Versioning
<!-- backward vs forward compatible changes. Adding an optional field is safe; renaming or removing is not. -->

## Schema Registry
<!-- central store of schemas (Avro/Protobuf), validates compatibility at publish time so a breaking change fails fast. -->

## Rules that keep you safe
<!-- never remove or repurpose a field, always default new ones, version the event type when you truly must break. -->

---
## 🔗 Connections
- **Prerequisite:** [[Kafka]]
- **Used by / relates to:** [[Event-Driven Architectures]] [[Database Migration Patterns]]
- **Contrast with:** [[API Design]]

#messaging #review
