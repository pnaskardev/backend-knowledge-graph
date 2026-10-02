---
aliases: [Clustered Index, Secondary Index, Composite Index, Covering Index]
---
# Indexing

> One article. Clustered vs secondary is the core split; composite and covering are refinements on top of it.

## Clustered Index
<!-- the index IS the table — leaves hold the full row. One per table. -->

## Secondary Index
<!-- leaves hold a pointer to the row, so a lookup costs a second hop. -->

## Composite Index
<!-- multi-column. Leftmost-prefix rule: why (a,b) serves a but not b. -->

## Covering Index
<!-- index holds every column the query needs, so the second hop is skipped entirely. -->

## Key trade-off
<!-- every index speeds reads and slows writes, and costs storage. -->

---
## 🔗 Connections
- **Prerequisite:** [[B+ Trees]]
- **Used by / relates to:** [[Transactions & Concurrency Control]] [[Sharding & Partitioning]]
- **Contrast with:** [[DynamoDB-style Stores]]

#databases #storage #review
