# How do you troubleshoot an application outage?

When I face an application outage, I first understand the impact of the issue, such as how many users are affected, which services are impacted, and whether it is a complete outage or a partial failure.

I then check monitoring tools like Splunk and Dynatrace to understand the application behavior, error patterns, and identify messages related to issues like network failures, DNS errors, authentication failures, or application errors.

As an SRE, my priority is to restore service as quickly as possible while identifying the root cause.

I follow a systematic troubleshooting approach. First, I check the infrastructure layer by validating CPU, memory, disk utilization, network health, and recent configuration changes or deployments.

If the infrastructure is healthy, I move to the application layer and check application logs, dependencies, database connectivity, authentication issues, or any recent application changes.

After identifying and fixing the issue, I validate that the application is reachable, transaction flow is normal, and monitoring alerts are cleared.

Finally, we perform RCA and implement preventive actions such as improving monitoring, adding validation steps before deployments, or automating checks to prevent similar incidents.
