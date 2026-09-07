A rate limiter restricts the intended or un-intended access to a system.

In this article we dive deep into the intuition between different types of rate limiting algorithms and their pros/cons.

For the sake of simplicity and understanding the concept of rate limiting we will be limiting requests on the basis of IP address.

Before we move forward we need to know what are the building blocks of a rate limiter.

## Components of a Rate Limiter

The Rate Limiter has the following components -

*   Configuration Store - to keep all of the rate limiting configurations
    
*   Request Store - to keep track of all the requests made against one configuration key
    
*   Decision Engine - it uses data from the Configuration Store and Request Store and makes the decision to either let the request pass or reject.
    

## Deciding Data stores

Picking the right data store for the use case is extremely important. The kind of data store we pick directly effects the kind of performance of a system like this.

### Configuration Store

The primary role of the Configuration Store would be to

*   efficiently store configuration for a key
    
*   efficiently retrieve the configuration for a key
    

In case of machine failure, we would not want to lose the configurations created, hence we choose a disk-backed data store that has an efficient `get` and `put` operation for a key. Since there would be billions of entries in this Configuration Store, using a SQL DB to hold these entries will lead to a performance bottleneck and hence we go with a simple key-value NoSQL database like [**MongoDB**](https://mongodb.com/) or [**DynamoDB**](https://aws.amazon.com/dynamodb/) for this use case.

### Request Store

Request Store will hold the count of requests served against each key per unit time. The most frequent operations on this store will be

*   registering (storing and updating) requests count served against each key - *write heavy*
    
*   summing all the requests served in a given time window - *read and compute heavy*
    
*   cleaning up the obsolete requests count - *write heavy*
    

Since the operations are both read and write-heavy and will be made very frequently (on every request call), we chose an in-memory store for persisting it. A good choice for such operation will be a data store like [**Redis**](https://redis.io/) but since we would be diving deep with the core implementation, we would store everything using the common data structures available.

## High Level Design of a Rate Limiter

The overall high-level design of the entire system looks something like this

![](https://cdn.hashnode.com/uploads/covers/680b2e2ed7a8f4e519cfd4fe/4a6d9f3d-3f66-40ec-babb-c0580acda062.png align="center")

## Token Bucket Rate Limiting

This type of algorithm holds a fixed number of tokens in a bucket. Tokens are added to the bucket at a configured fixed rate.

Each incoming requires one or more tokens to be processed.

If there are enough tokens available, the request is allowed and the tokens are removed.

If there are not enough tokens available, the request is rejected.

The bucket has a maximum capacity, and if the bucket is full, any new tokens that are added are discarded.

## Fixed Window Algorithm

This algorithm divides time into fixed intervals and counts the requests made within each interval.

For example - an API may allow 100 requests in a time interval of 5 minutes.

So between 10:00:00 and 10:05:00 the user will be able to make 100 requests, and everything beyond that gets rejected until the next window begins.

```go
const limit = 100
const window time.Duration = time.Duration(time.Minute * 5)
```

This is what our limit threshold and window interval look like.

In this case we are taking an interval of 5 minutes.

Every request that comes to the server is first checked, and the current time interval is calculated - which basically gives us the start of the current window.

With that window start we build our Fixed Window Rate Limiting key.

Here is how the key helper looks like -

```go
func FixedWindowKey(ip string, windowStart time.Time) string {
	return fmt.Sprintf("ratelimit:fixed:%s:%d", ip,     windowStart.Unix())
}
```

On this key we set a counter to 0

Every time a request is made within the same interval, we first increment the counter in Redis.

We then compare the counter against our threshold to check whether the user should be allowed or not, and make a decision accordingly.

## Sliding Window Log Rate Limiting

This algorithm is similar to the Fixed Window Rate Limiting algorithm, but instead of keeping a counter, we keep a log of all the requests made within the current window.

### Visualizing the window

Every time a request is made, we make a decision to either serve it or not; hence we check the `number of requests` made in the last `time_window_sec` seconds and compare it against our threshold.

So this process of checking a fixed window of time on every request is what gives this algorithm its name - Sliding Window Log Rate Limiting.

![](https://cdn.hashnode.com/uploads/covers/680b2e2ed7a8f4e519cfd4fe/3b3977f5-b926-47c2-b295-a0d7ac3cb714.png align="center")

## Leaky Bucket Rate Limiting

The leaky bucket is an algorithm based on an analogy of how a bucket with a constant leak will overflow if either the average rate at which water is poured in exceeds the rate at which the bucket leaks or if more water than the capacity of the bucket is poured in all at once.  
  
A counter associated with each user transmitting on a connection is incremented whenever the user sends a packet and is decremented periodically. If the counter exceeds a threshold upon being incremented, the network discards the packet. The user specifies the rate at which the counter is decremented (this determines the average bandwidth) and the value of the threshold (a measure of burstiness)

![](https://cdn.hashnode.com/uploads/covers/680b2e2ed7a8f4e519cfd4fe/3f1bb371-9443-4d0d-9765-aa7ebacfa6c3.png align="center")

Here is the intuition behind the leaky bucket rate limiting algorithm  
  
I have implemented the code for all of these above explained rate limiting algorithms in here - [https://github.com/pnaskardev/ratelimit-lab](https://github.com/pnaskardev/ratelimit-lab)

Thanks for reading!!



## 🔗 Connections

- [[Rate Limiter]]
- [[Backpressure]]
- [[API Gateway]]

#scaling #review
