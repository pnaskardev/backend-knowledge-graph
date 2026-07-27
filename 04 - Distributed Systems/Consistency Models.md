### What if Consistency ?
Consistency is essentially the capability of getting a non error response of the data which was the latest write. When multiple copies of data exist, what are users allowed to observe?
### When does inconsistency happen
Suppose you are building your own Instagram and you are at a very early position, all of your data is being stored in a single computer (which is exactly how Facebook started, Mark Zuckerberg used to store all of the data in a single computer).

One day you decide that you want to change your Bio so you make a change

the change is 

```
I am Batman ----> I am Iron Man
```

Since there is only one copy of data and a single database, everyone sees the same data, and the data which is being provided is consistent.

But real problems occur when you scale up and one computer is just not enough and you have a global audience now, you need to serve data across continents.

In this case having a single server to server traffic globally has 3 major problems - 
- Single point of failure 
- Latency is very high
- High cost of vertical scaling

So to tackle all of this, you decided to keep copies of your data across the continents to solve all of these failure points.

So now the database server looks like this 

```
                ┌── Database A (Bangalore)
User ──────────►│
                ├── Database B (London)
                │
                └── Database C (New York)
```

Now suppose you did the same operation of changing the bio again.

```
I am Iron Man ----> I am Batman
```

```
Database A → "I am Batman"  NEW-DATA

Database B → "I am Iron man"  OLD-DATA

Database C → "I am Iron man"  OLD-DATA

```

And now we have a consistency problem in front of us which we need to solve.

When we distributed our data, our different servers have different sets of realities of data.

### How do we solve this problem

#### Strong Consistency / Linearizable
Suppose you have a bank account.

and your current balance is `100 INR`

Now you try to deduct `80 INR` from your wallet and you successfully transact as well.

Your request hits Server A and you wallet balance goes from 
```
100 INR --> 20 INR
```

Immediately you reopen your banking app and your request hits a different server which had stale data and it shows.

```
Server B:

Balance = INR 100
```

For these kind of banking servers we often want very strong guarantee and then consistency model is called linearizability.

The intuition is - 
```
Once an operation is done succesfully, every later operation behaves as though the operation has already happened every where.
```

Even if there are other Database Nodes where the data might be inconsistent, the system behaves in such a way that there is only one correct copy.

To achieve this there are some protocols such as `Raft and Paxos consensus algorithm` used to build these kind of strong guarantees.

But since these algorithms involves a lot of coordination, strong consistency isn't always the best option.

It highly depends on the use case. 
#### Eventually Consistent
Now let us try to imagine something much less dangerous and which is not really related to banking operations.

You change you Instagram profile picture and there are multiple servers world wide serving the data.

Server A receives the data and this results in 
```
Server a -- New Profile Picture
Server b -- Old Profile Picture
Server c -- old Profile Picture
```

all of those people who are connected to Server a will see the update immediately and someone elsewhere might temporarily see the old profile picture.

And then replication happens and now all of the servers across the world has the latest update that was made.

In here the intuition is -

```
If no new updates happen, all replicas will eventually converge to the same data.
```

```
NOTE -It does not guarantee that every write happens and everyone will see immediately.
```

This way the system as whole may not be very consistent but definitely available.
#### Read your writes
Now to understand this lets think of an example where we are changing our profile picture on Instagram.

I changed my username from - 

```
priyanshu123 ---> Batman123
```

and my request went to Server A, but when I tried to refresh the maybe my request went to Server B and since replication hasn't reached Server B I will be seeing old data.

The core intuition in here is - 
```
After I update something i wont later read an older version of my own update.
```
#### Sequential

#### Causal


## 🔗 Connections
- **Prerequisite:** [[CAP Theorem]] [[PACELC]]
- **Used by / relates to:** [[Quorum Reads and Writes]] [[Replication]] [[MVCC]]
- **Contrast with:** [[Isolation Levels]]
- **Applied in:** [[Distributed Cache]] [[News Feed]]

#distributed-systems #review
