🟣 Question : What did your day look like in your recent role at Mastercard?


In my recent role at Mastercard, my day typically started with reviewing system health dashboards using Splunk and Dynatrace to ensure all critical services were stable, especially our IBM Sterling platform running on EKS.

I would then check any overnight alerts or incidents and prioritize them based on severity. If there were any ongoing issues, I would take ownership or coordinate with the relevant teams to resolve them quickly.

A significant part of my day involved working on CI/CD pipelines using Jenkins and GitHub Actions — optimizing builds, improving deployment reliability, and supporting application teams with release activities.

I also spent time troubleshooting Kubernetes-related issues such as pod failures, rollout issues, or IAM access problems, ensuring the platform maintained high availability.

Collaboration was a key part of my role — I regularly worked with developers, QA, and security teams for deployments, incident resolution, and performance improvements.

Additionally, I focused on automation tasks using Python and Bash to reduce manual effort, and contributed to improving observability by refining alerts and dashboards.

If there were any incidents, I was involved in L2/L3 support, root cause analysis, and ensuring long-term fixes were implemented.

Overall, my day was a mix of operational stability, automation, continuous improvement, and cross-team collaboration.


# 🟣 Follow-up Interview Questions (Based on Mastercard Role)

## 🔍 Incident Handling & RCA
- Can you walk me through one critical incident you handled end-to-end? What was the root cause?

Ans - ## 🟣 Critical Incident Story (End-to-End RCA) — Mastercard Experience

In my role at Mastercard, I was involved in a critical production incident impacting one of our core transaction-processing services running on **EKS (Kubernetes)** supporting **IBM Sterling workloads**.

---

### 🚨 Situation
During peak traffic hours, we observed a sudden degradation in system health through **Dynatrace alerts and Splunk dashboards**, including:
- Increased API latency
- Spike in 5xx error rates
- Multiple pod restarts across services

This directly impacted transaction processing flows, making it a high-priority production incident.

---

### 🎯 Task
My responsibility was to:
- Quickly identify the root cause
- Restore service stability as fast as possible
- Coordinate across DevOps, application, and infrastructure teams
- Ensure minimal business impact and prevent recurrence

---

### ⚙️ Action

#### 1. Initial triage (first 10–15 minutes)
- Checked Kubernetes cluster health (pods, nodes, deployments, HPA metrics)
- Identified multiple pods in **CrashLoopBackOff state**
- Determined issue was not isolated to a single node or namespace

#### 2. Log & metrics analysis
- Used **Splunk logs** and **Kubernetes event logs**
- Observed repeated authentication timeout errors between microservices
- Verified CPU/memory usage was normal → ruled out resource exhaustion

#### 3. Cross-team collaboration
- Engaged application + platform engineering teams immediately
- Correlated issue with a recent production deployment
- Identified changes in service-to-service authentication configuration

#### 4. Root cause identification
- Found misconfigured **IAM role-to-service-account mapping in EKS**
- This caused intermittent authentication failures between microservices used in transaction flows

#### 5. Mitigation steps
- Rolled back the recent deployment using **Jenkins CI/CD pipeline**
- Restarted affected deployments
- Stabilized traffic flow across services

#### 6. Validation
- Monitored **Dynatrace + Splunk dashboards**
- Confirmed:
  - Error rates returned to baseline
  - Latency normalized
  - Pod restarts stopped

---

### 📌 Result
- Service fully restored within a short incident window
- No data loss or transaction corruption occurred
- Improved MTTR through fast coordination and clear ownership

Post-incident improvements:
- Added validation checks for IAM/service-account mappings in CI/CD
- Enhanced monitoring for authentication failure patterns
- Improved alerting and dashboards for early detection
- Strengthened deployment review process

---

### 🧠 Root Cause
The root cause was a **misconfigured IAM role-to-service-account mapping during a recent deployment**, which led to intermittent authentication failures between microservices in the EKS-based architecture.
- How do you decide when to escalate an incident vs continue troubleshooting yourself?
- What was the most complex production issue you debugged in Kubernetes?
- How do you ensure incidents don’t repeat after RCA? Can you give an example?
- What was your MTTR improvement contribution in your role?

## ☸️ Kubernetes & Platform Engineering
- What were the most common causes of pod failures in your EKS environment?
- How did you troubleshoot a failed deployment in Jenkins + Kubernetes pipeline?
- How do you handle IAM or permission issues in a multi-service EKS setup?
- What steps do you take when a rollout gets stuck or goes into CrashLoopBackOff?
- How did you ensure high availability for IBM Sterling on EKS?

## 🔄 CI/CD & Automation
- What specific improvements did you make to your Jenkins or GitHub Actions pipelines?
- How did you reduce deployment failures or rollback frequency?
- Can you describe an automation script you built that saved significant manual effort?
- How do you ensure CI/CD pipelines are secure and compliant?
- What was the biggest bottleneck in your release process and how did you fix it?

## 📊 Observability & Monitoring
- What kind of alerts did you consider “noise” and how did you tune them?
- How do you differentiate between infrastructure vs application issues using Splunk/Dynatrace?
- What metrics did you consider critical for system health in your dashboards?
- How did you improve observability in your platform over time?
- Can you describe a situation where better monitoring would have prevented an incident?

## 🤝 Collaboration & Ownership
- Can you give an example where you coordinated multiple teams during a high-pressure issue?
- How do you handle disagreements with developers or QA during incident resolution?
- What does “taking ownership” mean to you in production support?
- How do you prioritize multiple incidents happening at the same time?
- How do you ensure smooth communication during outages?

## ⚙️ SRE Mindset & Reliability Engineering
- What improvements did you make that had a direct impact on system reliability?
- How do you balance new feature releases vs production stability?
- What was the most impactful automation you built in your role?
- How do you proactively prevent incidents instead of reacting to them?
- If you joined a new team tomorrow, what would you improve in the first 30 days?

## 🔥 Senior / Staff-Level Questions
- What would you redesign in your current platform if you had full ownership?
- What is the biggest reliability risk in a Kubernetes-based banking system like Mastercard?
- How do you ensure security and reliability together in CI/CD pipelines?
- What trade-offs have you made between speed of deployment and system stability?
- What is the most important lesson you learned from production incidents?
How do you proactively prevent incidents instead of reacting to them?
If you joined a new team tomorrow, what would you improve in the first 30 days?
🔥 Senior-level probing questions
What would you redesign in your current platform if you had full ownership?
What is the biggest reliability risk in a Kubernetes-based banking system like Mastercard?
How do you ensure security and reliability together in CI/CD pipelines?
What trade-offs have you made between speed of deployment and system stability?
What is the most important lesson you learned from production incidents?
