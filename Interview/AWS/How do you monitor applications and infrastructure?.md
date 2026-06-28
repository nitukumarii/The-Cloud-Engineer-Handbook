**How do you monitor applications and infrastructure?**


I primarily use CloudWatch for monitoring infrastructure and applications. I configure metrics, dashboards, and alarms for CPU, memory, disk utilization, network traffic, and application health. For Kubernetes workloads, I also monitor pod and node health along with application logs. During production incidents, I correlate CloudWatch metrics, application logs, Kubernetes events, and deployment history to quickly identify the root cause and restore service. I also use CloudTrail for auditing AWS API activities when investigating changes.
