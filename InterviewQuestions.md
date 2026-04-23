100 Interview Questions Based on the Sheet (Grouped & Practical)

**🟦 SRE & Reliability (1–20)**
What is the role of an SRE?
Difference between SRE and DevOps?
What are SLIs, SLOs, and SLAs?
How do you define error budgets?
How do you reduce MTTR?
Explain incident lifecycle.
What makes an alert actionable?
How do you avoid alert fatigue?
Describe a major production outage you handled.
How do you perform root cause analysis?
What is a blameless postmortem?
How do you ensure reliability before release?
How do you embed reliability in CI/CD?
What is toil? How do you reduce it?
How do you plan capacity?
How do you detect anomalies proactively?
Difference between monitoring and observability?
What metrics matter most for web apps?
How do you measure system health?
What’s your on-call experience?
**🟦 AWS & Cloud (21–40)**
Explain EC2 pricing models.
How do you optimize AWS costs?
Difference between ALB and NLB?
How does Auto Scaling work?
How do you design multi-AZ architecture?
IAM role vs policy?
How do you secure AWS infrastructure?
How do you monitor AWS services?
What is CloudWatch used for?
How do you manage secrets?
Difference between S3 and EBS?
RDS vs Aurora?
How do you design HA databases?
How do you handle AWS limits?
What is CloudFront?
How does CDN improve performance?
VPC components explained.
How do you debug network latency?
How do you isolate AWS incidents?
How do you handle region failure?
**🟦 Terraform & IaC (41–55)**
What is Infrastructure as Code?
Why Terraform over CloudFormation?
Explain Terraform state.
How do you manage state locking?
How do you structure Terraform modules?
How do you handle secrets in Terraform?
Terraform plan vs apply?
How do you manage multiple environments?
How do you perform Terraform rollback?
What are Terraform workspaces?
How do you version modules?
How do you avoid drift?
What is Terragrunt?
How do you enforce standards in IaC?
How do you review Terraform changes?
**🟦 CI/CD & Automation (56–70)**
Design a CI/CD pipeline.
Jenkins vs GitHub Actions?
What is GitOps?
How does Argo CD work?
Canary vs Blue-Green deployments?
How do you handle failed deployments?
How do you secure CI/CD pipelines?
How do you integrate scanning tools?
What causes pipeline failures?
How do you reduce deployment time?
How do you automate rollbacks?
CI/CD for Kubernetes?
How do you manage secrets in CI?
How do you test pipelines?
How do you scale CI/CD?
**🟦 Kubernetes & Containers (71–85)**
What happens when a pod crashes?
What is a Deployment vs StatefulSet?
How does HPA work?
What is Helm?
What is Ingress?
How do you expose services?
How do you secure Kubernetes?
RBAC explained.
How do you monitor EKS?
How do you troubleshoot pod issues?
What causes CrashLoopBackOff?
How do you manage config?
How do you handle upgrades?
What is node autoscaling?
How do you design HA on Kubernetes?
**🟦 Observability & Performance (86–100)**
What metrics do you monitor?
How does Prometheus work?
Datadog vs Prometheus?
What is log aggregation?
How do you trace latency issues?
What is RED / USE method?
How do you tune alerts?
How do you detect memory leaks?
How do you monitor Redis?
How do you scale Redis?
How do you improve web performance?
CDN cache hit ratio?
How do you isolate bottlenecks?
How do you plan load testing?
How do you prevent outages?


🟦 SRE & Reliability (1–20)
What is SRE and how is it different from DevOps?
How do you define SLIs and SLOs?
What is an error budget?
How do you reduce MTTR?
Walk me through a production incident you handled.
How do you prevent repeat incidents?
What makes a good alert?
How do you handle alert fatigue?
What is a blameless postmortem?
How do you prioritize reliability vs feature delivery?
How do you embed reliability in CI/CD?
What metrics indicate system health?
How do you plan capacity?
How do you detect anomalies early?
What is toil? How do you reduce it?
On-call experience?
How do you design for high availability?
Difference between monitoring and observability?
How do you handle customer-impacting incidents?
How do you document operational knowledge?
🟦 AWS & Cloud (21–40)
EC2 pricing models?
How do you optimize AWS costs?
ALB vs NLB?
How does Auto Scaling work?
IAM role vs policy?
How do you secure AWS infrastructure?
CloudWatch metrics vs logs?
S3 vs EBS vs EFS?
RDS HA options?
Multi-AZ vs Multi-region?
How does CloudFront work?
CDN cache invalidation?
VPC components?
NAT vs Internet Gateway?
Debugging network latency?
Handling region outage?
How do you monitor AWS services?
How do you manage secrets?
AWS limits and quotas?
Cost visibility tools you’ve used?
🟦 Terraform & IaC (41–55)
What is IaC?
Terraform vs CloudFormation?
Terraform state file?
State locking?
Modules vs workspaces?
Handling secrets in Terraform?
Terraform plan vs apply?
Rollback strategy?
Multi-environment setup?
Preventing drift?
Versioning modules?
Terraform best practices?
Handling failed applies?
Remote state?
Code review for Terraform?
🟦 CI/CD & Automation (56–70)
Design a Jenkins pipeline.
GitHub Actions vs Jenkins?
What is GitOps?
How does Argo CD work?
Canary vs blue-green?
Handling failed deployments?
Pipeline security?
Integrating scanning tools?
Reducing pipeline time?
Rollback automation?
CI/CD for Kubernetes?
Secrets in pipelines?
Pipeline monitoring?
Handling flaky builds?
CI/CD best practices?
🟦 Kubernetes & Containers (71–85)
Pod lifecycle?
Deployment vs StatefulSet?
HPA working?
What is Helm?
Ingress vs LoadBalancer?
RBAC explained?
CrashLoopBackOff causes?
Debugging pod issues?
Monitoring EKS?
Node autoscaling?
Securing Kubernetes?
ConfigMaps vs Secrets?
Rolling updates?
HA design in Kubernetes?
Upgrade strategy?
🟦 Observability & Performance (86–100)
Golden signals?
Prometheus architecture?
Datadog vs Prometheus?
Log aggregation strategy?
Tracing latency issues?
RED vs USE method?
Alert tuning?

Can you walk me through your experience with Red Hat Enterprise Linux?
How do you perform an OS installation on RHEL?
What is Red Hat Satellite and why is it used?
How do you register a server to Red Hat Satellite?
What is the difference between RPM and YUM?
How do you patch Linux servers in production with minimal downtime?
What steps do you follow to upgrade system software or firmware?
How do you manage kernel upgrades in RHEL?
What is SELinux and how do you troubleshoot SELinux issues?
How do you check system resource utilization in Linux?
Which command do you use to check CPU usage per process?
How do you tune Linux servers for performance?
What’s the difference between soft and hard limits in Linux?
How do you configure persistent routes in Linux?
How do you debug a high CPU usage issue on a Linux server?
How do you find which process is consuming high memory?
How do you configure swap space in Linux?
How do you reset a forgotten root password on RHEL?
What are systemd targets and how do you change the default target?
How do you configure and manage services with systemctl?
How do you schedule recurring jobs in Linux?
What is the difference between cron and systemd timers?
How do you check system logs in RHEL?
Which log files would you check if a server is not booting?
How do you troubleshoot a disk space issue?
How do you extend an LVM partition in Linux?
What’s the difference between ext4 and xfs filesystems?
How do you mount NFS on Linux?
How do you secure SSH access on a production server?
How do you set up SSH key-based authentication?
How do you analyze a core dump file in Linux?
How do you troubleshoot DNS resolution issues?
How do you configure hostname resolution without DNS?
How do you configure a static IP in Linux?
What is bonding and teaming in Linux networking?
How do you check open ports on a server?
How do you restrict access to a specific port in Linux?
What’s the difference between iptables and firewalld?
How do you configure firewalld to allow specific services?
How do you troubleshoot network latency on Linux?
How do you capture network packets for debugging?
What is the difference between TCP and UDP?
How do you configure time synchronization on RHEL?
How do you configure NTP or chrony service?
What’s the difference between runlevels and systemd targets?
How do you check what killed a process?
How do you find files modified in the last 24 hours?
How do you check file permissions in Linux?
What is the difference between symbolic and hard links?
How do you change file ownership recursively?
How do you find a specific string in multiple files?
How do you monitor real-time logs?
What’s the difference between tail -f and journalctl -f?
How do you configure auditd in Linux?
How do you ensure compliance of Linux servers?
How do you configure sudoers file securely?
How do you add a user with specific UID and GID?
How do you lock/unlock a user account?
How do you check last login history of a user?
How do you check if a user has sudo privileges?
How do you automate server builds with Ansible?
What is an Ansible playbook?
How do you use Ansible roles?
How do you secure sensitive data in Ansible?
What is the difference between Ansible and Puppet?
How do you test Ansible playbooks before running on production?
How do you integrate Ansible with Red Hat Satellite?
How do you handle idempotency in Ansible?
How do you debug errors in an Ansible playbook?
How do you write a Bash script to monitor disk space?
How do you pass arguments to a Bash script?
What’s the difference between “$*” and “$@” in Bash?
How do you schedule a Bash script to run automatically?
How do you handle errors in Bash scripts?
How do you write a script to restart a service if it fails?
How do you version control scripts with GitHub?
How do you create and merge branches in Git?
What’s the difference between Git merge and rebase?
How do you resolve Git conflicts?
How do you trigger CI/CD pipeline from GitHub commit?
How do you use GitHub Actions?
What’s the difference between Docker image and container?
How do you create a Dockerfile?
How do you run a container in detached mode?
How do you check logs of a Docker container?
How do you clean up unused Docker images and containers?
How do you create a custom Docker network?
What’s the difference between Docker volume and bind mount?
How do you push a Docker image to a registry?
How do you troubleshoot a failing container?
What’s the difference between Kubernetes and OpenShift?
How do you deploy an app on OpenShift?
What is an AKS cluster?
How do you scale pods in Kubernetes?
What’s the difference between Deployment and StatefulSet?
How do you configure secrets in Kubernetes?
How do you monitor Kubernetes clusters?
How do you troubleshoot a pod stuck in “CrashLoopBackOff”?
How do you perform disaster recovery for Linux servers?
Tell me about a time you solved a complex technical challenge under pressure.
Memory leak detection?
Redis monitoring?
Redis scaling?
Web performance tuning?
CDN cache hit ratio?
Bottleneck analysis?
Load testing strategy?
Preventing outages?
