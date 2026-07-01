# SAGAs to maintain data consistency in a microservice architecture
Before diving in, I want to give full credit to Chris Richardson, whose talk on Sagas is one of the clearest explanations of this pattern I've come across. This article draws heavily from that talk, you can watch it here [video][https://www.youtube.com/watch?v=YPbGW3Fnmbc&t=1317s]. My goal is simply to make those ideas accessible in a written, structured format.

In any microservice architecture, services collaborate mainly by exchanging transactional messaging.

Lets understand why do we need SAGAs - 

Let's imagine that you are working on an online store and customers have a credit limit.
```
invariant :- sum(open order.total)<= customer.creditLimit
```
It seems simple because we are used to building monolithic architectures.

## Transactions in a monolithic architecture

In a monolithic architecture the credit limit enforcement would look something like this.

```
BEGIN TRANSACTION

SELECT ORDER_TOTAL
	FROM ORDERS WHERE CUSTOMER_ID = ?

SELECT CREDIT_LIMIT
	FROM CUSTOMERS WHERE CUSTOMER_ID = ?

INSERT INTO ORDERS...

COMMIT TRANSACTION

```

Concurrent transactions for the customer will be serialized in a monolithic environment.

If there are concurrent transactions that attempt to order for the same customer, the properties of ACID transactions will make sure that this invariant is never violated.

But monolithic applications comes with a problem, which is called **monolithic hell** as the server codebase grows larger and larger.

This is the biggest motivation for the microservice architecture, instead of building something that is way to complex to develop test and deploy etc, we build a set of loosely coupled services which are simpler and fits in the head of a developer head.

It lets us parallelize service development.

![[IMG-20260521110053452.png]]
Loose data = encapsulate data

If services communicate via the database, they are no longer loosely couples.

Services are supposed to access one others data through APIs

## How to maintain Data consistency?

In this case we cannot use ACID transactions as we need to access other services data.

### 2 Phase Check 
- it guarantees consistency

**BUT** 
- PC coordinator is a single point of failure
- Chatty: At least On) messages, with retries O(n^2)
- Reduced throughput due to locks
- Not supported by many NoSQL databases (or message brokers)
- CAP theorem => 2PC impacts availibility.

### Use Sagas instead of 2PC
![[IMG-20260521112326644.png]]

![[IMG-20260521112534395.png]]

Breakup a ACID transactions in a sequence of local transactions.

### Rollback using compensation transactions

ACID can simply roll back

**BUT**
- Developer must write application logic to *rollback* eventually consistent transactions
- Careful design required.

Conceptually every one of the forward transactions has a corresponding undo transaction that undoes what it did.

You do `N` steps forward, then if the `N+1`th step fails you have to undo the N preceding steps.

![[IMG-20260523232826705.png]]


## Sagas complicate API Design and Business Logic

- Request initiates the SAGA. When to send back the response?
	- Option 1 : Send the response when SAGA completes:
		- PRO - Response specifies the outcome
		- CON - Reduced availability
	- Option 2 : Send response immediately after creating the saga (recommended):
		- PRO - Improved availability
		- CON - Response does not specify the outcome. Client must poll or be notified 
- Changes are committed by each step of the saga
- Other Transactions see `inconsistent` data, e.g - `Order.state="PENDING` => more complex logic.
- Interaction between SAGAs and other operation
	- e.g. What does it mean to cancel a PENDING order
	- "Interrupt" the create order saga.
	- Wait for the Create Order saga to complete?

## How to sequence the saga transaction

After the completion of the Ti "something" must decide what step to execute next.

Success - which T(i+1) - branching

Failure - C(i-1)

![[IMG-20260523234557700.png]]


- Choreography
	- ![[IMG-20260523234621231.png]]

- Orchestration - based coordination
	- ![[IMG-20260523234813031.png]]
	- Implicit vs. Explicit orchestrator
		- ![[IMG-20260523235356919.png]]
		- ![[IMG-20260523235433629.png]]'

Sagas are not always the right answer. If your data naturally lives in one service, a local ACID transaction is simpler and you should use it. Reach for Sagas when a business transaction genuinely spans multiple services and you cannot compromise on availability. Start with choreography for simple linear flows, and graduate to orchestration when the logic branches, requires rollback coordination, or becomes hard to trace. The goal is not to use Sagas everywhere,  it is to use them precisely where 2PC would hurt you most.


---
## 🔗 Connections
- **Prerequisite:** [[Database per Service]] [[Event-Driven Architectures]] [[Idempotency]]
- **Used by / relates to:** [[Transactional Outbox]] [[CQRS]]
- **Contrast with:** [[Transactions]]
- **Applied in:** [[Payment Gateway]] [[Food Delivery]]

#microservices #review
