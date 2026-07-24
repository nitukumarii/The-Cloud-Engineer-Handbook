# WirelessCar SRE Technical Round Preparation Report

## Date: 25/07/2026

## Category

Service Reliability Engineering

## Interview Stage

Technical Round

---

# Daily Goal

Prepare for the WirelessCar Technical Interview by focusing on the highest priority topics from the Job Description.

Today's Focus:

- Production Support
- Incident Management
- Major Incident Handling
- Automation
- CI/CD
- Infrastructure as Code
- Interview Communication

---

# Priority Based on JD

| Priority | Topic |
|----------|-------|
| ⭐⭐⭐⭐⭐ | Production Support & Incident Management |
| ⭐⭐⭐⭐⭐ | Linux Troubleshooting |
| ⭐⭐⭐⭐⭐ | Kubernetes Troubleshooting |
| ⭐⭐⭐⭐⭐ | RCA / PIR / Problem Management |
| ⭐⭐⭐⭐⭐ | Monitoring & Observability |
| ⭐⭐⭐⭐ | AWS Fundamentals |
| ⭐⭐⭐⭐ | REST API Troubleshooting |
| ⭐⭐⭐⭐ | Automation (Ansible, Bash) |
| ⭐⭐⭐⭐ | Jenkins / CI-CD |
| ⭐⭐⭐ | Kafka |
| ⭐⭐⭐ | Database Troubleshooting |
| ⭐⭐⭐ | Docker / Helm |

---

# Question Progress

| No | Question | Answer Created | Practiced | Confidence |
|----|----------|----------------|-----------|------------|
| 1 | Tell me about yourself (SRE focused) | ✅ | ❌ | - |
| 2 | Explain your Mastercard Production Environment | ✅ | ❌ | - |
| 3 | Explain your responsibilities as an SRE | ❌ | ❌ | - |
| 4 | Explain a major P1 Incident (Liveness Probe) | ✅ | ❌ | - |
| 5 | Explain a Sev1 Incident (Certificate Expiry) | ✅ | ❌ | - |
| 6 | Application outage troubleshooting | ✅ | ❌ | - |
| 7 | Application latency troubleshooting | ✅ | ❌ | - |
| 8 | High CPU troubleshooting | ✅ | ❌ | - |
| 9 | High Memory troubleshooting | ✅ | ❌ | - |
| 10 | Disk Full troubleshooting | ✅ | ❌ | - |
| 11 | DNS troubleshooting | ✅ | ❌ | - |
| 12 | Database timeout troubleshooting | ✅ | ❌ | - |
| 13 | REST API troubleshooting | ❌ | ❌ | - |
| 14 | Load Balancer unhealthy targets | ✅ | ❌ | - |
| 15 | Failed Production Deployment | ✅ | ❌ | - |
| 16 | Rollback Strategy | ❌ | ❌ | - |
| 17 | RCA Process | ✅ | ❌ | - |
| 18 | Post Incident Review (PIR) | ❌ | ❌ | - |
| 19 | Major Incident Management | ❌ | ❌ | - |
| 20 | Incident Commander Responsibilities | ❌ | ❌ | - |
| 21 | Change Management | ✅ | ❌ | - |
| 22 | Problem Management | ✅ | ❌ | - |
| 23 | Reduce MTTR | ✅ | ❌ | - |
| 24 | SLI vs SLO vs SLA | ✅ | ❌ | - |
| 25 | Error Budget | ✅ | ❌ | - |
| 26 | SRE Toil | ✅ | ❌ | - |
| 27 | Prevent recurring incidents | ✅ | ❌ | - |

---

# Automation

| No | Question | Answer Created | Practiced | Confidence |
|----|----------|----------------|-----------|------------|
| 28 | Why Automation? | ❌ | ❌ | - |
| 29 | Automation examples from your project | ✅ | ❌ | - |
| 30 | What operational activities can you automate? | ✅ | ❌ | - |
| 31 | Bash vs Python | ✅ | ❌ | - |
| 32 | Bash automation examples | ✅ | ❌ | - |
| 33 | Explain Ansible | ✅ | ❌ | - |
| 34 | Explain Inventory | ✅ | ❌ | - |
| 35 | Explain Playbook | ✅ | ❌ | - |
| 36 | Explain Roles | ✅ | ❌ | - |
| 37 | Automate patching using Ansible | ✅ | ❌ | - |
| 38 | Restart service only when configuration changes | ❌ | ❌ | - |
| 39 | Ansible Handlers | ❌ | ❌ | - |
| 40 | Terraform Workflow | ✅ | ❌ | - |
| 41 | Terraform State | ✅ | ❌ | - |
| 42 | Terraform Modules | ❌ | ❌ | - |
| 43 | Remote Backend | ❌ | ❌ | - |
| 44 | Infrastructure Drift | ❌ | ❌ | - |
| 45 | CI/CD Pipeline End-to-End | ✅ | ❌ | - |
| 46 | Jenkins Pipeline | ✅ | ❌ | - |
| 47 | Blue-Green vs Canary Deployment | ✅ | ❌ | - |
| 48 | Rollback after failed deployment | ❌ | ❌ | - |
| 49 | Infrastructure automation example | ❌ | ❌ | - |
| 50 | Automation improvements you introduced | ❌ | ❌ | - |

---

# Automation Scenario Practice

## Bash

- Automate log cleanup.
- Create a disk monitoring script.
- Restart a failed service automatically.
- Daily backup automation.
- Alert when disk usage exceeds 80%.

---

## Ansible

- Patch 500 Linux servers.
- Install Nginx on multiple servers.
- Update configuration files across all servers.
- Restart services only when configuration changes.
- Roll back failed configuration changes.
- Secure passwords using Ansible Vault.

---

## Terraform

- Provision AWS VPC and EC2.
- Deploy infrastructure using modules.
- Handle state file conflicts.
- Recover from infrastructure drift.
- Team collaboration using remote backend.

---

## Jenkins

- Build succeeds but deployment fails.
- Jenkins agent goes offline.
- Docker image push fails.
- Roll back production deployment.
- Pipeline fails after deployment.

---

# Production Follow-up Questions

These are the questions that usually differentiate a Senior SRE from a Mid-Level Engineer.

- How did you identify the root cause?
- Which logs did you check?
- Why did you use that command?
- What metrics confirmed the issue?
- How did you validate the fix?
- How did you reduce MTTR?
- What preventive action did you implement?
- How would you automate this process?
- What monitoring improvement would you add?
- What would you do if the issue happened again?

---

# Practice Status Legend

✅ Completed

🟡 Practiced but needs improvement

❌ Not Started

---

# Confidence Scale

5/10 → Understand concept

7/10 → Can explain

8/10 → Interview Ready

9/10 → Senior-level explanation

10/10 → Can handle follow-up questions confidently

---

# Answer Framework

## Production Scenarios

1. Understand the business impact.
2. Check monitoring dashboards.
3. Identify the affected layer.
4. Collect logs and evidence.
5. Identify the root cause.
6. Apply the fix.
7. Validate recovery.
8. RCA and prevention.

---

## Automation Questions

1. Business problem.
2. Tool selection.
3. Implementation.
4. Validation.
5. Benefits.
6. Future improvements.

---

# Commands to Revise

## Linux

```bash
top
ps -ef
free -m
vmstat
iostat
sar
journalctl
df -h
du -sh
ss -tulnp
lsof
systemctl
```

## Kubernetes

```bash
kubectl get pods
kubectl get nodes
kubectl describe pod
kubectl logs
kubectl get events
kubectl top pods
kubectl top nodes
kubectl rollout status
kubectl rollout undo
```

---

# Communication Focus

Today's focus is **communication**, not learning new tools.

Practice:

- Keep answers between **60–90 seconds**.
- Start every answer with a clear approach.
- Avoid filler words:
  - So...
  - Basically...
  - Actually...
  - Like...
- Speak with confidence and pause before answering.
- End every answer with:
  - Validation
  - Prevention
  - Business impact

---

# End of Day Target

- Complete all 50 questions.
- Practice all Production Support answers without notes.
- Practice all Automation scenarios.
- Record your answers and review communication.
- Achieve **8/10 confidence** on every Production Support question.
- Be able to answer follow-up questions without hesitation.
