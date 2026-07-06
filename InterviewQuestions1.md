# 🚀 DevOps / SRE / Cloud Interview Questions (Structured – No Repetition)

---

## 🟦 SRE & Reliability (1–20)

1. What is SRE and how is it different from DevOps?
2. What is the role of an SRE in production systems?
3. What are SLIs, SLOs, and SLAs?
4. What is an error budget and how is it used?
5. How do you reduce MTTR (Mean Time To Recovery)?
6. Explain the incident lifecycle.
7. What makes an alert actionable?
8. How do you avoid alert fatigue?
9. What is a blameless postmortem?
10. How do you perform root cause analysis?
11. How do you prevent repeat incidents?
12. How do you prioritize reliability vs feature delivery?
13. How do you embed reliability into CI/CD pipelines?
14. What is toil? How do you reduce it?
15. How do you plan capacity for systems?
16. How do you detect anomalies proactively?
17. Difference between monitoring and observability?
18. What metrics indicate system health?
19. How do you design systems for high availability?
20. How do you handle customer-impacting incidents?

---

## 🟦 AWS & Cloud (21–40)

21. Explain EC2 pricing models.
22. How do you optimize AWS costs?
23. Difference between ALB and NLB?
24. How does Auto Scaling work?
25. IAM role vs IAM policy?
26. How do you secure AWS infrastructure?
27. What is CloudWatch used for?
28. Difference between CloudWatch metrics and logs?
29. S3 vs EBS vs EFS?
30. RDS vs Aurora?
31. How do you design HA databases in AWS?
32. Multi-AZ vs Multi-region architecture?
33. What is CloudFront and how does it work?
34. How does CDN improve performance?
35. What are VPC components?
36. NAT Gateway vs Internet Gateway?
37. How do you debug network latency in AWS?
38. How do you handle AWS service limits and quotas?
39. How do you manage secrets in AWS?
40. How do you handle region failure?

---

## 🟦 Terraform & IaC (41–55)

41. What is Infrastructure as Code (IaC)?
42. Terraform vs CloudFormation?
43. What is Terraform state file?
44. How do you manage state locking?
45. Terraform modules vs workspaces?
46. How do you handle secrets in Terraform?
47. Terraform plan vs apply?
48. How do you manage multiple environments?
49. How do you perform Terraform rollback?
50. How do you prevent configuration drift?
51. How do you version Terraform modules?
52. What is Terragrunt?
53. What are Terraform best practices?
54. How do you handle failed Terraform apply?
55. What is remote state in Terraform?

---

## 🟦 CI/CD & Automation (56–70)

56. Design a CI/CD pipeline.
57. Jenkins vs GitHub Actions?
58. What is GitOps?
59. How does Argo CD work?
60. Canary vs Blue-Green deployments?
61. How do you handle failed deployments?
62. How do you secure CI/CD pipelines?
63. How do you integrate security scanning tools?
64. What causes pipeline failures?
65. How do you reduce deployment time?
66. How do you automate rollbacks?
67. CI/CD strategy for Kubernetes?
68. How do you manage secrets in CI/CD?
69. How do you test pipelines?
70. How do you scale CI/CD systems?

---

## 🟦 Kubernetes & Containers (71–85)

71. What happens when a pod crashes?
72. What is Pod lifecycle?
73. Deployment vs StatefulSet?
74. How does HPA work?
75. What is Helm?
76. What is Ingress?
77. Ingress vs LoadBalancer service?
78. How do you expose services in Kubernetes?
79. RBAC explained.
80. How do you secure Kubernetes clusters?
81. What causes CrashLoopBackOff?
82. How do you troubleshoot pod issues?
83. ConfigMaps vs Secrets?
84. How do you handle Kubernetes upgrades?
85. How do you design HA in Kubernetes?

---

## 🟦 Observability & Performance (86–100)

86. What are the golden signals of monitoring?
87. How does Prometheus work?
88. Datadog vs Prometheus?
89. What is log aggregation?
90. How do you trace latency issues?
91. What is RED vs USE method?
92. How do you tune alerts?
93. How do you detect memory leaks?
94. How do you monitor Redis?
95. How do you scale Redis?
96. How do you improve web performance?
97. What is CDN cache hit ratio?
98. How do you isolate bottlenecks?
99. How do you plan load testing?
100. How do you prevent outages?

---

## 🟦 Linux / RHEL / Scripting / DevOps (101–130)

101. What is the difference between RPM and YUM?
102. How do you patch Linux servers with minimal downtime?
103. How do you manage kernel upgrades?
104. What is SELinux and how do you troubleshoot it?
105. How do you check system resource utilization?
106. How do you debug high CPU usage?
107. How do you find high memory consuming processes?
108. How do you configure swap space?
109. How do you secure SSH access?
110. How do you configure firewalld?
111. iptables vs firewalld?
112. How do you troubleshoot disk space issues?
113. How do you extend LVM partitions?
114. How do you mount NFS?
115. How do you troubleshoot DNS issues?
116. How do you configure static IP?
117. How do you check open ports?
118. How do you capture network packets?
119. TCP vs UDP?
120. How do you configure time sync (NTP/chrony)?
121. What are systemd targets?
122. How do you manage services using systemctl?
123. How do you schedule jobs (cron)?
124. cron vs systemd timers?
125. How do you monitor logs in real time?
126. tail -f vs journalctl -f?
127. How do you configure auditd?
128. How do you manage users and permissions?
129. How do you automate with Ansible?
130. What is a Bash script and how do you use it?

---

## 🟦 Behavioral / Real Scenarios (131–150)

# 🟦 Behavioral & Production Scenarios (JRD Systems)

1. Tell me about a P1 production incident you handled from start to finish.

2. Describe the most challenging production outage you've resolved.

3. Tell me about a time you automated a repetitive operational task using Ansible, Bash, or Python.

4. Describe a production deployment that failed. How did you investigate and recover the service?

5. Tell me about a production issue where you performed Root Cause Analysis (RCA).

6. Describe an on-call incident where you restored a critical production service.

7. Tell me about a time you worked with developers to resolve a production issue.

8. Describe a situation where you had to troubleshoot an issue with limited information.

9. Tell me about a production change that had to be implemented with minimal or zero downtime.

10. Describe a production patching activity you were involved in.

11. Tell me about a time you prevented a recurring production issue through automation or monitoring improvements.

12. Describe a situation where monitoring tools such as Splunk, Dynatrace, or CloudWatch helped you identify the root cause.

13. Tell me about a performance issue you investigated in production.

14. Describe a situation where infrastructure was healthy but the application was failing. How did you identify the root cause?

15. Tell me about a time you handled multiple production incidents simultaneously. How did you prioritize them?

16. Describe your experience working with security teams during certificate renewals, vulnerability remediation, or production changes.

17. Tell me about a production rollback you performed. Why was rollback chosen instead of fixing the application?

18. Describe a time when you improved system reliability or reduced MTTR.

19. Tell me about a production incident that taught you an important lesson.

20. Why do you think you're a good fit for this Application Support Engineer role at JRD Systems?
---

# 🎯 One-Line Summary

This covers full stack:
SRE + AWS + Terraform + CI/CD + Kubernetes + Linux + Behavioral
