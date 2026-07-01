# Exponential Backoff
This solves the problem of request hammering the instance while the system is recovering,

Instead of hammering the instance the with 10K requests on regular time intervals lets increase the backoff time exponentially so that we give the instance some time to recover.

This still has some problems like - 
	What if is 10K clients fail together, in this case all 10K clients retry together at the same time with exponential backoff, even after adding delays.
	
The Solution is to add [[📝 Concepts/Jitter|Jitter]]

---
## 🔗 Connections
- **Prerequisite:** [[Retry Strategies]]
- **Used by / relates to:** [[Jitter]]

#reliability #distributed-systems #review
