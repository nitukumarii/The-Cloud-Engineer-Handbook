# Infrastructure is healthy but application is failing. How do you investigate?

If the infrastructure is healthy but the application is failing, I would first confirm the impact and understand the scope of the issue.

I would check monitoring tools like Dynatrace to analyze application-level metrics such as error rate, transaction failure rate, request flow, response time, and affected services to understand the failure pattern.

Since infrastructure metrics like CPU, memory, and disk are healthy, I would move my investigation to the application layer.

I would check application logs using tools like Splunk to identify errors, exceptions, authentication failures, configuration issues, or application-specific problems.

I would also verify dependencies such as database connectivity, third-party integrations, APIs, and downstream service availability.

If the issue started after a recent deployment or configuration change, I would review the change and coordinate with the application team for rollback or remediation.

After the fix, I would validate application availability, transaction flow, and monitoring alerts to confirm the service is fully recovered.
