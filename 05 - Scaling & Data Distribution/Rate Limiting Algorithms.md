A rate limiter restricts intended or unintended access to a system.

In this article we dive deep into the intuition behind the different types of rate limiting algorithms and their pros/cons.

For the sake of simplicity, and to keep the focus on the concept of rate limiting itself, we will be limiting requests on the basis of IP address.

Let us have a look at the different rate limiting algorithms popularly used by engineers around the world.

## Fixed Window Rate limiting

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

Against this key we keep a counter, starting at 0.

Every time a request is made within the same interval, we first increment the counter in Redis.

We then compare the counter against our threshold to check whether the user should be allowed or not, and make a decision accordingly.

## 🔗 Connections
- [[Rate Limiter]]
- [[Backpressure]]
- [[API Gateway]]

#scaling #review
