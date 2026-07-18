#topic #review
CAP Theorem is also known as Brewers Theorem named after the Computer Scientist who state the theorem Eric Brewer

When a network partition occurs, a distributed system must choose between Consistency and Availability. Partition Tolerance is not optional in a distributed system because partitions will eventually happen. 

We can't simply say that our I don't support partitions. If we have multiple databases running on multiple machines then network failures will happen.

CAP Theorem stands for -
- Consistency
	- Consistency in CAP theorem implies that every read it receives is the most recent write in the database
	- Consistency in ACID properties implies that the database goes from one consistent state to another consistent state with the help of some constraint values
- Availability
	- Every Request receives a non error response without the guarantee that it was the most recent write in the database.
	- We have excluded the criteria that its the most recent write.
- Partition Tolerance
	- The system continues to operate regardless of arbitrary number of messages being dropped between the nodes by the network.

When a partition failure happens there are two options we can take and any software engineer has to decide between these two - 

- Option A (CP system) -
	- In case of partition failure if I choose that my system should be consistency, I will be giving up on availability.
	- We can showcase this with a very simple example -
		Suppose we have two replicas of a database. A network partition occurs and the replicas can no longer communicate. A write reaches Replica A. 
		
		A read reaches Replica B. 
		
		To ensure the client never sees stale data, Replica B refuses the read request until communication is restored. The system remains consistent but sacrifices availability.
		
		This is called CP system.
		
- Option B (AP system) -
	- In case of partition failure if I choose that my system should be available, I will be giving up on consistency.
	- We can showcase this with a very simple example-
		
		Suppose we have two replicas. A network partition occurs after Replica A accepts a write. 
		
		Replica B has not yet received the update. 
		
		If Replica B continues serving read requests, clients may receive stale data. The system remains available but sacrifices consistency.
		
		This is called an AP system.

In absence of a network partition we can guarantee both Consistency and Availability.

But when would network partition really occur ?

Network partitions are inevitable in any distributed system, whether the nodes are located in the same data center or distributed across the world.

What this means is if you have a single node Postgres database so definitely network partition is not going to happen since there is only one node, CAP does not really apply because there are no network partitions between replicas. and you will have a highly consistent and available database.

If a network partition occurs, a CP system chooses to reject some requests to preserve consistency, while an AP system continues serving requests at the cost of consistency. 

So lets get one thing out of the way that Network Partitioning is inevitable.

We cannot completely avoid network partitions. However, we can significantly reduce their likelihood by using reliable hardware, redundant network paths, multiple switches and routers, monitoring systems, and fault-tolerant infrastructure.

CAP theorem isn't a checklist, it's a lens. The real skill isn't memorizing 'CP vs AP,' it's knowing which failure mode your business can tolerate: stale data, or no data. Next time you're choosing a database, that's the question you're actually answering.


---
## 🔗 Connections
- **Prerequisite:** [[Distributed Systems Trade-offs]]
- **Used by / relates to:** [[PACELC]] [[Consistency Models]] [[Quorum Reads and Writes]]
- **Contrast with:** [[PACELC]]
- **Applied in:** [[Replication]] [[DynamoDB-style Stores]]

#distributed-systems #review
