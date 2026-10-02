---
aliases: [Consensus Algorithms, Leader Election, Split Brain]
---
# Consensus & Leader Election

> One story: nodes must agree on a value → the common case is agreeing who leads → split brain is what happens when agreement fails.

## Consensus Algorithms
<!-- Raft, Paxos. Why a majority (quorum) is required, and why even numbers of nodes buy you nothing. -->

## Leader Election
<!-- the main use of consensus. Terms, heartbeats, what happens on leader failure. -->

## Split Brain
<!-- a partition leaves two leaders, both accepting writes. The failure consensus exists to prevent. Fencing tokens. -->

## Key trade-off
<!-- consensus costs a round trip to a majority on every write. That is the price of not having split brain. -->

---
## 🔗 Connections
- **Prerequisite:** [[CAP Theorem]] [[Quorum Reads and Writes]]
- **Used by / relates to:** [[Distributed Locking]] [[Failure Handling]] [[Replication]]
- **Contrast with:** [[Consistency Models]]

#distributed-systems #review
