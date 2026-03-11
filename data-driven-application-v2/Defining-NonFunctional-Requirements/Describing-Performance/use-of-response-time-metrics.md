# Response Time Distribution

Because response time varies from one request to the next, we need to think of it not as a single number, but as a distribution of values that we can measure.

In the figure below, each gray bar represents a request to a service, and the height shows how long that request took. Most requests are fast, but there are occasional outliers that take much longer.

<img width="363" height="162" alt="Response time distribution chart" src="https://github.com/user-attachments/assets/e34ea79d-321d-40b4-8229-2f93c3a94cd2" />

It's common to report the average response time of a service. The mean response time is useful for estimating throughput limits.

It's best to use percentiles to understand a "typical" response time. A good approach is to use the median by sorting the response times. The median is also known as the 50th percentile, or p50.

High response-time percentiles, also known as **tail latencies**, are important because they directly affect users' experience of the service.

## Tail Latency Amplification

High percentiles are especially important in backend services that are called multiple times as part of serving a single end-user request. Even if you make the calls in parallel, the request still needs to wait for the slowest of the parallel calls to complete — meaning it takes just one slow call to make the entire end-user request slow.

Even if only a small percentage of backend calls are slow, the chance of getting a slow call increases if an end-user request requires multiple backend calls, so a higher proportion of such end-user requests end up being slow. This is known as **tail latency amplification**.

<img width="349" height="212" alt="Tail latency amplification diagram" src="https://github.com/user-attachments/assets/e3820fe4-a6b2-488f-9b22-d2f3d170696d" />

