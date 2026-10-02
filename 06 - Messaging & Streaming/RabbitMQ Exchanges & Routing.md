---
aliases: [Exchange, Binding, Routing Key, Direct Exchange, Fanout Exchange, Topic Exchange, Headers Exchange]
---
# RabbitMQ Exchanges & Routing

> One mechanism, four flavours. A producer never writes to a queue — it writes to an exchange, and bindings decide where the message lands.

## The routing model
<!-- Producer → Exchange → (Binding + Routing Key) → Queue → Consumer. Draw this once and the four exchange types are obvious. -->

## Binding & Routing Key
<!-- binding = the rule connecting an exchange to a queue. Routing key = the label on the message that the rule matches against. -->

## Direct Exchange
<!-- exact match on routing key. -->

## Fanout Exchange
<!-- ignores the routing key, copies to every bound queue. This is pub/sub. -->

## Topic Exchange
<!-- pattern match with `*` (one word) and `#` (zero or more). The flexible default. -->

## Headers Exchange
<!-- match on header attributes instead of the routing key. Rarely needed. -->

## Which to use
<!-- direct for work routing, fanout for broadcast, topic for everything else. -->

---
## 🔗 Connections
- **Prerequisite:** [[RabbitMQ]] [[Message Queue Fundamentals]]
- **Used by / relates to:** [[Dead Letter Queues & Poison Messages]]
- **Contrast with:** [[Kafka]] [[Kafka vs RabbitMQ]]

#messaging #rabbitmq #review
