# Failure Handling

**One-liner:** 
	In Microservices creating an order talks to multiple services and any of these microservices may fail at any time due to maybe 
		- DB Lock
		- Container Restarting
		- Network Timeout
		- DNS issues
	Anything can happen at any time 
### Transient Failures
These are temporary problem and can be fixed by just retrying and waiting for some time.

Examples - 
	- Network hiccup
	- CPU spike
	- DB Lock
### Permanent Failures
These are the failures which cannot be solved by just retrying. 
For example lets say that there is a user account which was not found, in this case retrying wont do anything cause by retrying the account wont reappear magically.

## Partial Failures
Only some of the components are down not everything is down.
This results in system inconsistency.

## Slow Failures
The system us just slow and nothing else.

---
## 🔗 Connections
- **Prerequisite:** [[Distributed Systems Trade-offs]]
- **Used by / relates to:** [[Retry Strategies]] [[Circuit Breaking Concepts]] [[Bulkhead Pattern]] [[Timeout Pattern]]
- **Applied in:** [[Payment Gateway]]

#distributed-systems #review
