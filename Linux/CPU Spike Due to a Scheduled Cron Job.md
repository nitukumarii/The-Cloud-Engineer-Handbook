# Interview Question: CPU Spike Due to a Scheduled Cron Job

## Question

**Interviewer:** Suppose you find that the CPU spike is caused by a scheduled cron job. Since the job runs every day, would you still investigate it?

## Answer

Yes, I would verify it first before concluding that it is normal behavior. A scheduled cron job causing a CPU spike is often expected, but I don't assume it is healthy just because it is scheduled.

First, I confirm that the CPU spike coincides with the scheduled execution time of the cron job by checking the cron schedule and historical monitoring dashboards. Then I compare the current CPU utilization and job duration with previous executions.

If the cron job behaves as expected—for example, CPU utilization increases for a few minutes, the job completes successfully, application response times remain normal, there are no error-rate increases, and users are not impacted—I consider it normal operational behavior. In this case, no immediate action is required other than continued monitoring.

However, if I notice that the CPU utilization is significantly higher than usual, the job takes longer to complete, starts consuming excessive system resources, or impacts application performance, I investigate further. Possible reasons could include increased data volume, inefficient code, resource contention, infrastructure bottlenecks, or changes introduced by a recent deployment.

As an SRE, I never assume that a scheduled task is healthy simply because it is expected. I always verify that it is performing within its normal baseline and not affecting production services.

---

## Key Interview Takeaway

**Expected does not always mean healthy.**

A scheduled CPU spike is acceptable **only if**:

- It occurs at the expected time.
- It lasts for the expected duration.
- CPU returns to its normal baseline.
- The application continues to meet its SLOs.
- Users are not impacted.
- No abnormal errors or alerts are generated.

If any of these conditions change, it should be investigated as a potential production issue.
