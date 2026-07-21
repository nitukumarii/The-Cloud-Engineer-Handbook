# Application is slow — how do you investigate?

If an application becomes slow, I first understand the impact, such as which users are affected, when the issue started, and whether it is a complete slowdown or a specific transaction flow.

I check monitoring tools like Dynatrace and Splunk to analyze metrics such as response time, latency, error rate, throughput, and request patterns.

Before troubleshooting, I create possible hypotheses because application slowness can happen due to multiple reasons, such as increased traffic during peak hours, resource exhaustion, scheduled jobs, database performance issues, or dependency failures.

I start by checking the infrastructure layer, including CPU, memory, disk utilization, and network health.

If infrastructure looks healthy, I move to the application layer and check application logs, database connectivity, API response times, and third-party dependency performance.

For network-related issues, I verify DNS resolution, connectivity, and latency.

After identifying the root cause and applying the fix, I validate application response time and confirm that performance has returned to normal.
