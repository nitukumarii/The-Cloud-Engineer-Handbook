# AWS Production Issue Resolved - High CPU on EC2 Instance (STAR)

## Situation

While working in TCS, we faced a production issue where an application hosted on an AWS EC2 instance started responding slowly during business hours.

Monitoring alerts showed increased CPU utilization, and users experienced slow application response.

## Task

As part of the infrastructure support team, my responsibility was to identify the root cause, restore application performance, and minimize the impact on users.

## Action

I first checked CloudWatch metrics to understand the issue and confirmed that CPU utilization was consistently high.

I logged into the EC2 instance and checked system-level metrics using Linux commands like `top`, `ps`, and `vmstat` to identify the process consuming high CPU.

I identified that a background process was consuming excessive resources and impacting application performance.

I coordinated with the application team to validate whether the process was required and safely restarted the service after approval.

After the restart, I monitored CloudWatch metrics, application logs, and server health to confirm that CPU utilization and response time returned to normal.

## Result

The application performance was restored, CPU utilization returned to normal levels, and the incident was resolved within the SLA.

As a preventive measure, we improved monitoring thresholds and reviewed resource utilization trends to avoid similar issues.
