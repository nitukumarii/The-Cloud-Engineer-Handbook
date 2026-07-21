Application
↓
Architecture
↓
Monitoring
↓
My Responsibility
↓
Common Issues
↓
Goal


# Describe Your Production Environment

## Answer

The production environment I supported at Mastercard was a **payment file transfer platform built around IBM Sterling B2B Integrator**, which was responsible for securely transferring payment files between Mastercard and partner banks.

The platform was a **distributed system** consisting of IBM Sterling, Java Spring Boot backend services, React frontend, databases, and integrations with multiple downstream banking systems. The application components were hosted on **AWS EKS Kubernetes cluster**.

For monitoring and observability, we used **Splunk and Dynatrace**.

- Splunk was mainly used for log analysis and troubleshooting application issues.
- Dynatrace was used for application performance monitoring, including response time, error rate, transaction flow, and dependency monitoring.

We monitored infrastructure metrics like:
- CPU
- Memory
- Disk
- Network

Application metrics like:
- Response time
- Error rate
- Transaction success/failure
- Availability

Kubernetes metrics like:
- Pod health
- Pod restarts
- Container resource usage

As an SRE, my responsibilities included monitoring production, handling P1/P2 incidents, performing RCA, supporting deployments, troubleshooting application and Kubernetes issues, and automating repetitive tasks using Bash and Python.

Common production issues we handled were deployment failures, pod crashes, application latency, file transfer delays, certificate expiry issues, and downstream connectivity problems.

Overall, my role was to maintain application reliability, availability, and stability while reducing MTTR and ensuring successful payment processing.
