“My core experience is in Site Reliability Engineering, where I’ve been responsible for maintaining and improving reliability of production systems, especially in Kubernetes and AWS environments.

I’ve worked extensively on incident response, reducing MTTR, and ensuring high availability for critical systems like Mastercard’s file transfer platform.

Alongside that, I’ve used DevOps practices like CI/CD pipelines, Terraform, and automation — but primarily to improve system reliability, deployment safety, and operational efficiency.

So I would position myself as an SRE with strong DevOps and platform engineering experience.”



🎯 Fidelity System Explanation (Your Case)
🧩 What the system was

At Fidelity, you worked on:

In-house investor inventory platforms

These systems typically:

Track investor data
Handle portfolio / transaction records
Support internal business operations
🔗 Real Architecture (very realistic)
Flow:
User / internal system triggers request
Application services running on Kubernetes (EKS) process requests
Backend services:
Fetch / update investor data
Handle business logic
Data stored in databases
Monitoring + alerting across system
☁️ Where your work fits (SRE view)

You were responsible for:

Kubernetes workload reliability (EKS)
Performance and scalability
Observability (Datadog, Prometheus, Grafana)
SLO/SLI definition
Incident handling



At Fidelity, I worked on internal investor inventory platforms running on AWS EKS. These systems handled critical investor data and required high reliability and performance.

My role focused on managing Kubernetes workloads, improving observability, and defining SLIs and SLOs to ensure system health. I also worked on performance testing and infrastructure provisioning using Terraform, enabling scalable and consistent environments.

I contributed to incident response and proactive monitoring, which helped improve issue detection and system stability.”

in depth
“The system was fully containerized and deployed on EKS, where different services handled investor data processing and internal workflows.

I was responsible for ensuring reliability at the infrastructure and platform level — including cluster operations, observability, and performance validation.

By implementing SLO-driven monitoring and improving alerting, we were able to detect issues earlier and improve overall system reliability.”


“At Fidelity, I ensured reliability and performance of Kubernetes-based internal platforms handling investor data, focusing on observability, SLOs, and scalable infrastructure.


Experience

Senior Site Reliability Engineer with 7+ years of experience operating and improving reliability of high-scale, cloud-native systems across AWS and Kubernetes environments. Proven track record of maintaining 99.9%+ availability for critical production platforms, reducing MTTR through effective incident response, and implementing observability-driven improvements using modern monitoring stacks. Extensive experience designing resilient infrastructure, enhancing deployment safety through CI/CD and Infrastructure as Code (Terraform), and driving automation to eliminate manual operational overhead. Strong background in leading incident triage, performing root cause analysis, and implementing long-term reliability improvements in 24x7 production environments. Collaborates closely with engineering and platform teams to build scalable, fault-tolerant systems, with a focus on operational excellence, system resilience, and continuous improvement.

Mastercard
•	Owned reliability of a business-critical IBM Sterling file transfer platform, enabling secure financial data exchange across global banking systems.
•	Maintained 99.9%+ availability for AWS EKS workloads by proactively resolving rollout failures, pod instability, and IAM-related access issues in production .
•	Improved deployment reliability by ~40% by optimizing CI/CD pipelines using Jenkins and GitHub Actions with controlled rollout and rollback strategies .
•	Led L2/L3 incident response for IBM Sterling platform, diagnosing Kubernetes, network, and access-related failures in real time, reducing MTTR by ~30% .
•	Defined and aligned SLIs/SLOs for critical services, improving observability standards and enabling proactive detection of reliability issues .
•	Automated operational workflows using Python and Bash, reducing manual effort by ~80% and minimizing recurring operational risks .
•	Led enterprise certificate lifecycle management using Venafi across EMEA, US, and India regions, ensuring secure renewals, compliance, and zero service disruption .
•	Enhanced observability using Splunk and Dynatrace, improving issue detection, alert correlation, and root cause analysis efficiency .
•	Contributed to blameless postmortems and RCA, implementing long-term fixes to prevent recurring production failures and improve system resilience.
