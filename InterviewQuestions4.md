# 🚀 Monitoring + AWS + DevOps Interview Notes (Structured & Clean)

---

# 🟦 1. IT Monitoring Fundamentals (1–10)

1. What is ITIL?  
ITIL is a framework for IT Service Management (ITSM) that standardizes incident, problem, and change management.  
👉 Helps monitoring by defining alert handling, SLAs, and incident workflows  

2. What is RMM (Remote Monitoring & Management)?  
Tools to monitor, manage, and automate IT infrastructure remotely  
👉 Features:
- Alerts
- Patch management
- Remote troubleshooting  

3. SNMP vs WMI  
SNMP → Network devices (routers, switches)  
WMI → Windows systems monitoring  

4. Firewall vs Switching  
Firewall → Controls traffic (security rules)  
Switch → Routes data inside network using MAC  

5. What is Active Directory?  
Microsoft directory service for:
- Authentication
- Authorization
- User management  

6. Role of VMware  
Virtualization platform → runs multiple VMs on one server  

7. Proactive vs Reactive Monitoring  
Proactive → Prevent issues before impact  
Reactive → Fix after failure  

8. What is monitoring policy?  
Rules + thresholds + alerts for system health  

9. Why monitoring is important?  
- Prevent downtime  
- Improve performance  
- Ensure reliability  

10. Key monitoring metrics  
CPU, Memory, Disk, Network, Latency  

---

# 🟦 2. Monitoring Hands-On (11–18)

11. Configure monitoring for global infra  
- Identify critical services  
- Define thresholds  
- Enable alerts  
- Use dashboards  
- Review regularly  

12. SNMP troubleshooting  
- Check SNMP service  
- Verify community string  
- Query using SNMP tool  
- Analyze OIDs  

13. Handle performance issue  
- Check CPU/memory/disk  
- Analyze logs  
- Restart/scale if needed  

14. Monitor Windows Servers  
- WMI  
- Event Viewer  
- Performance Monitor  

15. Critical alert handling  
- Identify impact  
- Check logs  
- Fix or escalate  

16. Access-based roles  
- RBAC  
- Least privilege  

17. Configure RMM  
- Install agents  
- Set alerts  
- Enable automation  

18. Firewall rule setup  
- Allow required ports  
- Block unwanted traffic  

---

# 🟦 3. Scenario-Based Monitoring (19–24)

19. App slow but no alerts  
- Check logs  
- Check DB queries  
- Network latency  
- Manual testing  

20. Alert flooding (major outage)  
- Identify root cause  
- Suppress duplicate alerts  
- Fix core issue  

21. Monitoring gaps  
- Add missing alerts  
- Improve thresholds  
- Enhance dashboards  

22. Design scalable monitoring  
- Centralized logging  
- Distributed monitoring  
- Auto-scaling alerts  

23. Multi-client incident handling  
- Prioritize critical  
- SLA-based response  

24. Security policy changes  
- Implement RBAC  
- Test before rollout  

---

# 🟦 4. Behavioral (25–29)

25. Major incident handling  
- Identify → Fix → RCA  

26. Handling multiple tasks  
- Prioritize  
- Automate  

27. Monitoring gap fix  
- Add alerts → prevent failure  

28. Unknown issue handling  
- Research + escalate  

29. Documentation  
- Runbooks + knowledge sharing  

---

# 🟦 5. AWS Networking (30–35)

30. VPC Peering vs Transit Gateway vs PrivateLink  
Peering → simple VPC connect  
Transit → hub model  
PrivateLink → private service access  

31. NAT Gateway  
Allows private subnet → internet access  

32. Security Group vs NACL  
SG → instance level (stateful)  
NACL → subnet level (stateless)  

33. Connectivity troubleshooting  
- SG/NACL  
- Routes  
- DNS  

34. AWS Load Balancers  
ALB → HTTP  
NLB → TCP  
CLB → legacy  

35. Network latency debugging  
- CloudWatch  
- Flow logs  

---

# 🟦 6. AWS Compute & Storage (36–40)

36. EC2 instance selection  
Based on CPU, memory, workload  

37. Spot vs On-Demand vs Reserved  
Spot → cheap  
On-demand → flexible  
Reserved → long-term  

38. EBS vs EFS vs S3  
EBS → block  
EFS → shared  
S3 → object  

39. Migrate EC2 → Lambda  
- Refactor app  
- Stateless design  

40. S3 lifecycle  
Move data → cheaper storage  

---

# 🟦 7. AWS Security (41–45)

41. IAM (Users, Roles, Policies)  
Controls access  

42. Least privilege  
Only required permissions  

43. KMS vs Secrets Manager  
KMS → encryption  
Secrets → credentials  

44. Data security  
- Encryption at rest  
- TLS in transit  

45. EC2 compromise  
- Isolate  
- Rotate keys  
- Investigate logs  

---

# 🟦 8. AWS DevOps (46–50)

46. IaC  
Infrastructure via code  

47. Terraform structure  
Modules + environments  

48. Parameter Store vs Secrets Manager  
Params → config  
Secrets → sensitive  

49. Patch EC2  
SSM automation  

50. Drift detection  
Detect config changes  

---

# 🟦 9. Kubernetes / EKS (51–60)

51. EKS  
Managed Kubernetes  

52. Pod networking  
VPC CNI  

53. Deployment  
Manages pods  

54. HPA vs CA  
HPA → pods  
CA → nodes  

55. Logging  
CloudWatch / ELK  

56. Storage  
EBS / EFS  

57. Security  
IAM + RBAC  

58. Troubleshoot pod  
logs + describe  

59. Multi-AZ  
High availability  

60. Best practice  
Rolling updates  

---

# 🟦 10. AWS Monitoring (61–65)

61. CloudWatch vs CloudTrail  
CloudWatch → metrics/logs  
CloudTrail → API logs  

62. EC2 metrics  
CPU, network, disk  

63. Lambda logs  
CloudWatch  

64. X-Ray  
Tracing tool  

65. VPC Flow logs  
Network analysis  

---

# 🟦 11. Serverless (66–70)

66. SNS vs SQS vs EventBridge  
SNS → push  
SQS → queue  
EventBridge → event routing  

67. Lambda idempotency  
Avoid duplicate execution  

68. Cold start  
Startup delay  

69. Retry policies  
Automatic retries  

70. High availability  
Multi-AZ  

---

# 🟦 12. AWS Security Advanced (71–75)

71. GuardDuty  
Threat detection  

72. API Gateway security  
Auth + WAF  

73. WAF  
Protect web apps  

74. Security Hub  
Central security view  

75. Macie  
Data classification  

---

# 🟦 13. Cost Optimization (76–80)

76. EC2 cost optimization  
Right-size + auto-scale  

77. Savings Plans  
Long-term discount  

78. Cost Explorer  
Analyze billing  

79. S3 optimization  
Lifecycle + tiering  

80. Trusted Advisor  
Recommendations  

---

# 🟦 14. AWS Troubleshooting (81–85)

81. High CPU EC2  
Check processes  

82. Slow RDS  
Check queries  

83. AWS limits  
Request increase  

84. IAM issues  
Policy debugging  

85. Disaster recovery  
Backup + failover  

---

# 🟦 15. Real Troubleshooting Scenarios (86–90)

86. EC2 → RDS issue  
Check SG, NACL, routes  

87. High latency  
CloudWatch + logs  

88. Lambda timeout  
Check VPC + timeout  

89. Cost spike  
Analyze + optimize  

90. DDoS attack  
WAF + Shield  

---

# 🟦 16. Storage Lifecycle (91–95)

91. S3 lifecycle  
Auto tiering  

92. EFS lifecycle  
Move to IA  

93. EBS  
No lifecycle  

94. Snapshot strategy  
Backup  

95. Cost saving  
Delete unused  

---

# 🎯 Final Summary

Monitoring + AWS + DevOps =  
👉 Observability + Automation + Security + Cost Optimization + Reliability
