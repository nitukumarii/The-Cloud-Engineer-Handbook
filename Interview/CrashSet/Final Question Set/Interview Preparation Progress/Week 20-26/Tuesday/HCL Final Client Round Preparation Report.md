
# HCL Final Client Round Preparation Report

## Date: 21/07/2026

## Category:
Production Support / Site Reliability Engineering

## Interview Stage:
Final Client Round


# Daily Goal

Prepare high-impact SRE production support scenarios focusing on:

- Incident Management
- Kubernetes troubleshooting
- Application troubleshooting
- Monitoring and Observability
- AWS troubleshooting
- CI/CD
- Ansible automation
- Database basics
- SRE principles
- Mastercard project discussion


---

# Question Progress


| No | Question | Answer Created | Practiced | Confidence |
|----|----------|----------------|-----------|------------|
| 1 | Tell me about yourself | ✅ | ✅ |  8/10 |
| 2 | Describe your production environment | ✅ | ✅ |  7/10 |
| 3 | Explain the last application you worked on at Mastercard - flow, upstream, downstream | ✅ | ✅ |  7/10 |
| 4 | What was your major role in Mastercard project? | ✅ | ✅ |  7/10 |
| 5 | Describe a major P1 production incident you handled | ✅ | ✅ |  7/10 |
| 6 | Tell me about a Sev1 incident | ✅ | ✅ |  7/10 |
| 7 | How do you troubleshoot an application outage? | ✅ |  ✅  | 8/10 |
| 8 | Infrastructure is healthy but application is failing - how do you investigate? | ✅ |  ✅  | 8/10 |
| 9 | Application is slow - how do you investigate? | ✅ |  ✅  | 7/10 |
| 10 | How do you troubleshoot increased API latency using Grafana? | ❌ | ❌ | - |
| 11 | Kubernetes application has high latency - which Linux commands do you use? | ❌ | ❌ | - |
| 12 | Pod crashes during P1 incident - troubleshooting approach | ❌ | ❌ | - |
| 13 | Kubernetes pod continuously restarting - how do you troubleshoot? | ❌ | ❌ | - |
| 14 | How do you troubleshoot high CPU? | ✅ | 🟡 | 5/10 |
| 15 | How do you troubleshoot memory issues? | ✅ | 🟡 | 6/10 |
| 16 | Disk is full - troubleshooting approach | ✅ | 🟡 | 6/10 |
| 17 | DNS resolution failure troubleshooting | ✅ | 🟡 | 6/10 |
| 18 | Load balancer unhealthy targets troubleshooting | ✅ | 🟡 | 7/10 |
| 19 | Database connection timeout troubleshooting | ✅ | 🟡 | 7/10 |
| 20 | EC2 to RDS connectivity troubleshooting | ✅ | ✅ |  8/10 |
| 21 | SQL/RDBMS experience explanation | ✅ | ✅ |  8/10 |
| 22 | Identify blocking processes in SQL | ✅ | ✅ |  7/10 |
| 23 | Production database backup precautions |✅ | ✅ |  8/10 |
| 24 | Certificate management issue handled | ✅ | ✅ |  8.5/10 |
| 25 | Monitoring tools experience (Splunk, Dynatrace, CloudWatch, Grafana) | ✅ | ✅ |  8/10 |
| 26 | How do you reduce alert fatigue? | ✅ | ✅ |  8/10 |
| 27 | Splunk search vs stats vs eval |  ✅ | ✅ |  8/10 |
| 28 | How do you collect and analyze logs? |  ✅ | ✅ |  8.5/10 |
| 29 | Jenkins pipeline issue handled | ✅ | ✅ |  7.5/10 |
| 30 | How do you handle production deployments? | ✅ |  ✅  | 7/10 |
| 31 | How do you handle failed deployments? |  ✅ | ✅ |  8.5/10 |
| 32 | Blue-Green vs Canary deployment | ✅ | ✅ |  8.5/10 |
| 33 | CI/CD pipeline design | 8.5/10 |
| 34 | Why Ansible instead of shell scripting? | ✅ | ✅ |  8/10 |
| 35 | Explain Ansible playbook | ✅ | ✅ |  8/10 |
| 36 | Explain Ansible roles | ✅ | ✅ |  8/10 |
| 37 | Automate patching using Ansible | ✅ | ✅ |  8/10 |
| 38 | Terraform workflow | ✅ | ✅ |  8/10 |
| 39 | Terraform state | ✅ | ✅ |  8/10 |
| 40 | AWS production issue resolved |  ✅ | ✅ |  8/10 |
| 41 | AWS observability services | ✅ | ✅ |  6/10 |
| 42 | AWS security best practices | ✅ | ✅ |  8/10 |
| 43 | Error Budget explanation | ✅ | ✅ |  8/10 |
| 44 | SLI, SLO, SLA explanation |  ✅ | ✅ |  8/10 |
| 45 | How do you reduce MTTR? | ✅ | ✅ |  6/10 |
| 46 | Explain SRE toil |  ✅ | ✅ |  6/10 |
| 47 | What operational activities can you automate? | ✅ | ✅ |  8.5/10 |
| 48 | Change Management vs Problem Management | ✅ | ✅ |  8.5/10 |
| 49 | CVRT incident understanding | ❌ | ❌ | - |
| 50 | How do you ensure recurring incidents are permanently resolved? | ✅ | ✅ |  8/10 |


---

# Practice Status Legend

✅ Completed  
🟡 Practiced but needs improvement  
❌ Not started


Confidence:

5/10 → Understand concept

7/10 → Can explain

8/10 → Interview ready

9/10 → Strong senior-level answer


---

# Answer Framework To Follow


For Production Scenarios:


## 1. Understand Impact

- Which application?
- Which users?
- Production impact?
- Business impact?


## 2. Check Monitoring

Tools:

- Splunk
- Dynatrace
- CloudWatch
- Grafana


## 3. Identify Layer

Check:

- Application
- Kubernetes
- Infrastructure
- Database
- Network
- Dependency


## 4. Collect Evidence

Use:

- Logs
- Metrics
- Events
- Recent deployments
- Configuration changes


## 5. Mitigation

Examples:

- Rollback deployment
- Restart service
- Scale resources
- Failover
- Fix configuration


## 6. Prevention

- RCA
- Monitoring improvement
- Automation
- Documentation


---

# Commands To Revise


## Kubernetes

```bash
kubectl get pods
kubectl describe pod
kubectl logs
kubectl get events
kubectl top pods
kubectl top nodes
