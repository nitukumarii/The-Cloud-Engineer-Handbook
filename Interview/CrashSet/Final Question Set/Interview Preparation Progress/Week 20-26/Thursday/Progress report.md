# WirelessCar SRE Preparation Report

## Date: 23/07/2026

## Category:

Production Support / Automation / Site Reliability Engineering

## Daily Goal

Strengthen production support troubleshooting and automation concepts while improving communication, confidence, and structured answers for Senior SRE interviews.

Focus Areas:

* Production Incident Management
* Troubleshooting Methodology
* Automation Scenarios
* CI/CD
* Infrastructure as Code
* Interview Communication

---

# Question Progress

| No | Question                                                        | Answer Created | Practiced | Confidence |
| -- | --------------------------------------------------------------- | -------------- | --------- | ---------- |
| 1  | Explain a major P1 incident (Liveness Probe Failure)            | ✅              | ❌         | -          |
| 2  | Explain a Sev1 incident (Certificate Expiry)                    | ✅              | ❌         | -          |
| 3  | Application outage troubleshooting                              | ✅              | ❌         | -          |
| 4  | Slow application troubleshooting                                | ✅              | ❌         | -          |
| 5  | High CPU troubleshooting                                        | ✅              | ❌         | -          |
| 6  | High Memory troubleshooting                                     | ✅              | ❌         | -          |
| 7  | Disk full troubleshooting                                       | ✅              | ❌         | -          |
| 8  | DNS resolution failure                                          | ✅              | ❌         | -          |
| 9  | Database connection timeout                                     | ✅              | ❌         | -          |
| 10 | Load Balancer unhealthy targets                                 | ✅              | ❌         | -          |
| 11 | Failed production deployment                                    | ✅              | ❌         | -          |
| 12 | Rollback strategy                                               | ❌              | ❌         | -          |
| 13 | Production deployment validation checklist                      | ❌              | ❌         | -          |
| 14 | Root Cause Analysis (RCA) process                               | ✅              | ❌         | -          |
| 15 | How do you reduce MTTR?                                         | ✅              | ❌         | -          |
| 16 | Change Management vs Problem Management                         | ✅              | ❌         | -          |
| 17 | SLI vs SLO vs SLA                                               | ✅              | ❌         | -          |
| 18 | Error Budget                                                    | ✅              | ❌         | -          |
| 19 | Explain SRE Toil                                                | ✅              | ❌         | -          |
| 20 | How do you ensure recurring incidents are permanently resolved? | ✅              | ❌         | -          |
| 21 | What operational activities can you automate?                   | ✅              | ❌         | -          |
| 22 | AWS production issue handled                                    | ✅              | ❌         | -          |
| 23 | Production support responsibilities as an SRE                   | ❌              | ❌         | -          |
| 24 | Production deployment lifecycle                                 | ❌              | ❌         | -          |
| 25 | Major Incident handling process                                 | ❌              | ❌         | -          |

---

# Automation

| No | Question                                        | Answer Created | Practiced | Confidence |
| -- | ----------------------------------------------- | -------------- | --------- | ---------- |
| 26 | Bash vs Python                                  | ✅              | ❌         | -          |
| 27 | Bash automation examples                        | ✅              | ❌         | -          |
| 28 | Automate log cleanup using Bash                 | ❌              | ❌         | -          |
| 29 | Automate health check script                    | ❌              | ❌         | -          |
| 30 | Cron jobs                                       | ❌              | ❌         | -          |
| 31 | Explain Ansible                                 | ✅              | ❌         | -          |
| 32 | Explain Inventory                               | ✅              | ❌         | -          |
| 33 | Explain Playbook                                | ✅              | ❌         | -          |
| 34 | Explain Roles                                   | ✅              | ❌         | -          |
| 35 | Automate patching using Ansible                 | ✅              | ❌         | -          |
| 36 | Update configuration across multiple servers    | ❌              | ❌         | -          |
| 37 | Restart service only when configuration changes | ❌              | ❌         | -          |
| 38 | Secure passwords using Ansible Vault            | ❌              | ❌         | -          |
| 39 | Terraform workflow                              | ✅              | ❌         | -          |
| 40 | Terraform state                                 | ✅              | ❌         | -          |
| 41 | Terraform modules                               | ❌              | ❌         | -          |
| 42 | Terraform remote backend                        | ❌              | ❌         | -          |
| 43 | Infrastructure drift                            | ❌              | ❌         | -          |
| 44 | CI/CD pipeline end-to-end                       | ✅              | ❌         | -          |
| 45 | Jenkins pipeline stages                         | ✅              | ❌         | -          |
| 46 | GitHub Actions workflow                         | ✅              | ❌         | -          |
| 47 | ArgoCD deployment flow                          | ✅              | ❌         | -          |
| 48 | Blue-Green vs Canary deployment                 | ✅              | ❌         | -          |
| 49 | Failed deployment recovery                      | ❌              | ❌         | -          |
| 50 | Infrastructure automation in your project       | ❌              | ❌         | -          |

---

# Automation Scenario Practice

* Automate patching for 200 Linux servers.
* Deploy Nginx across all servers using Ansible.
* Roll back a failed Ansible deployment.
* Restart services only when configuration changes.
* Provision a VPC and EC2 using Terraform.
* Handle Terraform state conflicts in a team environment.
* Build and deploy an application using Jenkins.
* GitHub Actions deployment to EKS.
* ArgoCD deployment becomes OutOfSync.
* CI/CD deployment fails after Docker image creation.
* Automate certificate renewal.
* Automate log cleanup and rotation.
* Automate daily infrastructure health checks.
* Automatically restart failed services.
* Automate backup and validation.

---

# Practice Status Legend

✅ Completed

🟡 Practiced but needs improvement

❌ Not started

---

# Confidence Scale

5/10 → Understand concept

7/10 → Can explain with guidance

8/10 → Interview ready

9/10 → Senior-level explanation

10/10 → Can handle follow-up questions confidently

---

# Answer Frameworks

## Production Support

1. Understand business impact.
2. Check monitoring and alerts.
3. Identify the affected layer.
4. Collect logs and evidence.
5. Find the root cause.
6. Implement the fix.
7. Validate recovery.
8. RCA and prevention.

---

## Automation Questions

1. Problem to solve.
2. Tool selected and why.
3. Implementation approach.
4. Validation.
5. Benefits.
6. Improvements.

---

# Commands to Revise

## Linux

```bash
top
ps aux
free -m
vmstat
iostat
sar
journalctl
df -h
du -sh
ss -tulnp
netstat
lsof
systemctl
```

## Kubernetes

```bash
kubectl get pods
kubectl describe pod
kubectl logs
kubectl get events
kubectl top pods
kubectl top nodes
kubectl rollout status
kubectl rollout undo
```

---

# Communication Goals (Highest Priority)

Today's focus is not learning more tools—it is improving interview delivery.

* Keep answers between **60–90 seconds**.
* Pause for 2 seconds before answering.
* Avoid filler words:

  * "So..."
  * "Basically..."
  * "Actually..."
  * "Like..."
* Follow a structured approach instead of thinking aloud.
* Every answer should end with the outcome or benefit.

---

# End of Day Target

* Complete all 50 questions.
* Record answers for the top 15 production support questions.
* Practice 10 automation scenarios without notes.
* Achieve a minimum confidence score of **8/10** for every topic before moving to the next module.
