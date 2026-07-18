# Event-Driven Architectures, the why, how and what

When people first start to build microservices they tend to build REST interfaces around everything and we end up with big long call chains and potentially increased latency and worse is if the Service B is down and Service A is trying to make a call, this makes sure that we have missed the event.

Its a good idea in this case that we have some sort of buffer to manage these scenarios.

These kind of problems are typically solved by a event driven architectures.

Microservices communicate primarily with events, with APIs where required
- Microservices can produce and consume events using publish/subscribe messaging.
- Events are handled by an event backbone 
- Data is always eventually consistent
![[Pasted image 20260608005224.png]]

Lets try to compare messaging patterns

## Point to Point 

- Point to Point is basically a Java Messaging Service term
- The point to point way of thinking about things is that we use a queue as an intermediate kind of structure, where the producers send messages to the queue and we and up with an ordered list
- Consumers pick each message a does the processing part, each message is consumed by a single consumer.
- This is a good way of sharing messages but not particularly a very good way of kind of spreading events across multiple microservices in which we want to process.
- ![[Pasted image 20260608005938.png]]

## Publish/Subscribe

- Instead of having a queue in the middle we have something called a topic(Kafka) / Exchange (RabbitMQ).
- We can have multiple subscriptions on the same topic, and each subscription gets their own copy.
- Since we have two subscriptions(given in the diagram) it's processed twice and this is a good way of fanning messages out.
- This is the more loosely coupled way of service communication and I can add a subscription and add a new consumer and kind of enhance the application without changing the producer side of the application.
- ![[Pasted image 20260608010425.png]]


## Event Backbone
![[Pasted image 20260608010758.png]]

In this example we have 2 microservices as we can see.

One Microservice is producing the messages and one microservice has subscription to a topic and it is consuming the messages.

Because this is a asynchronous ofcourse the execution rate of the consumer can be different and the consumer needs to process all of the messages in aggregate at roughly the same rate but if you have kind of peaks and troughs in the rate of the producer then it doesn't effects the performance of the consumer.

We can also  perform maintenance on the consumer we can just stop it temporarily upgrade the version restart and we can start processing the events and nothing is lost.

## What we need to build an event driven microservices ?

Identify the following 
- Events
- Actors
- Data
- Commands
What we will get is a set of micro services with the events that they want to respond to and start implementing the pieces of it.








---
## 🔗 Connections
- **Prerequisite:** [[Message Queue]] [[Publish Subscribe]]
- **Used by / relates to:** [[CQRS]] [[SAGA Pattern]] [[Transactional Outbox]] [[Event Driven Architecture]]
- **Applied in:** [[Notification Service]] [[News Feed]]

#microservices #review
