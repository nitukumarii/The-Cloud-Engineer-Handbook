### How do you collect and analyze logs? 




In my previous project, we integrated observability tools like Splunk and Dynatrace for monitoring and troubleshooting.

Splunk was mainly used for log analysis, where we analyzed application and system logs to identify errors, exceptions, and failure patterns.

Dynatrace was used for application performance monitoring, where we monitored metrics like transaction failures, error rate, response time, throughput, and overall application health.

During production incidents, we usually correlated Dynatrace metrics with Splunk logs to understand when the issue started, the impact of the issue, the exact error message, and the failure point.

For example, Dynatrace helped us identify the affected service and failure pattern, while Splunk helped us find the detailed error logs and root cause.
