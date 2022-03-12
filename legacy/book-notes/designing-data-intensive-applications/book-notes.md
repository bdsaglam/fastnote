
## Chapter 1: Reliable, Scalable, and Maintainable Applications

- A fault is usually defined as one com‐ ponent of the system deviating from its spec, whereas a failure is when the system as a whole stops providing the required service to the user. 

- Although we generally prefer tolerating faults over preventing faults, there are cases where prevention is better than cure (e.g., because no cure exists). This is the case with security matters, for example: if an attacker has compromised a system and gained access to sensitive data, that event cannot be undone.

- Fan-out: In transaction processing systems, we use it to describe the number of requests to other services that we need to make in order to serve one incoming request.

- High percentiles become especially important in backend services that are called multiple times as part of serving a single end-user request. Even if you make the calls in parallel, the end-user request still needs to wait for the slowest of the parallel calls to complete. It takes just one slow call to make the entire end-user request slow, as illus‐ trated in Figure 1-5. Even if only a small percentage of backend calls are slow, the chance of getting a slow call increases if an end-user request requires multiple back‐ end calls, and so a higher proportion of end-user requests end up being slow (an effect known as tail latency amplification [24]).
If you want to add response time percentiles to the monitoring dashboards for your services, you need to efficiently calculate them on an ongoing basis. For example, you may want to keep a rolling window of response times of requests in the last 10 minutes. Every minute, you calculate the median and various percentiles over the val‐ ues in that window and plot those metrics on a graph.
The naïve implementation is to keep a list of response times for all requests within the time window and to sort that list every minute. If that is too inefficient for you, there are algorithms that can calculate a good approximation of percentiles at minimal CPU and memory cost, such as forward decay [25], t-digest [26], or HdrHistogram [27]. Beware that averaging percentiles, e.g., to reduce the time resolution or to com‐ bine data from several machines, is mathematically meaningless—the right way of aggregating response time data is to add the histograms [28].

- Moseley and Marks [32] define complexity as accidental if it is not inherent in the problem that the software solves (as seen by the users) but arises only from the implementation.

## Chapter 3: Storage and Retrieval

## Chapter 5: Replication

### Leader - Follower

There are two kinds of replicaton strategies: synchronous or asynchronous.
In sync replication, leader waits replication to followers complete, which guarantees
that any data is present in multiple nodes. However, in async replication, leader 
doesn't wait replication to finish and hence, there is a risk of data loss, if leader
fails before any replication happens. In practice, mixture of sync and async replication
is preferred, called semi-synchronous replication. 