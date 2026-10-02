---
aliases: [Read Replicas]
---
# Replication

> Same data on more than one node. Read replicas are the most common reason you do it.

## Why replicate
<!-- read scaling, availability, geographic locality. Three different goals, different setups. -->

## Leader–follower (single leader)
<!-- all writes to the leader, followers stream the log. The default. -->

## Multi-leader & leaderless
<!-- writes anywhere; now you need conflict resolution and quorums. -->

## Read Replicas
<!-- scale reads by pointing them at followers. The catch: replication lag means read-your-own-writes breaks. -->

## Sync vs async
<!-- sync costs write latency, async risks losing acknowledged writes on failover. -->

---
## 🔗 Connections
- **Prerequisite:** [[CAP Theorem]] [[Consistency Models]]
- **Used by / relates to:** [[Sharding & Partitioning]] [[Consensus & Leader Election]] [[Quorum Reads and Writes]]
- **Applied in:** [[Distributed Cache]]

#scaling #review
