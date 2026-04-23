**AWS Infrastructure & Networking**

1. **Explain the differences between VPC Peering, Transit Gateway, and PrivateLink. When would you use each?**

   * **VPC Peering**: A direct network connection between two VPCs that allows them to communicate as if they were on the same network. It’s best for simple, point-to-point connections between a limited number of VPCs.
   * **Transit Gateway**: A central hub that connects multiple VPCs and on-premises networks, reducing the complexity of managing multiple peering connections. Used for large-scale, multi-VPC architectures.
   * **PrivateLink**: Enables private connectivity between VPCs and AWS services without exposing traffic to the public internet. Ideal for secure SaaS applications and cross-account services.

2. **How does an AWS NAT Gateway work, and when should you use it?**

   * NAT Gateway allows instances in a private subnet to initiate outbound traffic to the internet while preventing inbound connections. It is useful when private instances need to access external services (e.g., OS updates) without exposing them to the internet.

3. **What are the differences between Security Groups and NACLs?**

   * **Security Groups**: Operate at the instance level, are stateful (allow return traffic), and evaluate all rules before deciding whether to allow traffic.
   * **Network ACLs**: Operate at the subnet level, are stateless (each request and response is evaluated separately), and rules are evaluated in order.

4. **How do you troubleshoot connectivity issues between two AWS resources in different VPCs?**

   * Check VPC peering, Transit Gateway, or PrivateLink settings.
   * Verify route tables and ensure proper routes exist.
   * Confirm Security Group and NACL configurations.
   * Use VPC Flow Logs to analyze traffic.
   * Perform a traceroute to check connectivity paths.

5. **Explain the different types of Load Balancers in AWS and when to use them.**

   * **Application Load Balancer (ALB)**: Best for Layer 7 (HTTP/HTTPS) traffic, supports host-based and path-based routing.
   * **Network Load Balancer (NLB)**: Best for Layer 4 (TCP/UDP) traffic, handles high-performance applications with low latency.
   * **Classic Load Balancer (CLB)**: Older generation, supports both Layer 4 and Layer 7 but lacks advanced routing features.

**Compute & Storage**

6. **How do you choose the right EC2 instance type for a given workload?**

   * **General Purpose (T3, M5)**: Balanced for various workloads.
   * **Compute Optimized (C5, C6g)**: CPU-intensive applications.
   * **Memory Optimized (R5, X1e)**: Applications requiring high RAM.
   * **Storage Optimized (I3, D3)**: Workloads needing high disk I/O.
   * **GPU Instances (P4, G5)**: Machine learning, gaming, and AI.

7. **What are the benefits of Spot Instances vs. On-Demand Instances vs. Reserved Instances?**

   * **Spot Instances**: Up to 90% cheaper than On-Demand but can be terminated anytime.
   * **On-Demand Instances**: Pay per hour, no long-term commitment.
   * **Reserved Instances**: Up to 75% discount for long-term commitments (1–3 years).

8. **Explain the differences between EBS vs. EFS vs. S3.**

   * **EBS (Elastic Block Store)**: Persistent block storage for EC2, suitable for databases.
   * **EFS (Elastic File System)**: Managed file storage, scales automatically.
   * **S3 (Simple Storage Service)**: Object storage, ideal for backups and big data.

9. **How would you migrate an application running on an EC2 instance to AWS Lambda?**

   * Refactor code into stateless microservices.
   * Move configurations to AWS Systems Manager Parameter Store.
   * Replace direct database access with API Gateway + DynamoDB.
   * Optimize dependencies to reduce cold start times.

10. **What are S3 lifecycle policies, and how do you optimize storage costs using them?**

* Lifecycle policies automatically transition objects between S3 storage classes (Standard -> IA -> Glacier) based on age.
* Helps reduce costs by storing infrequently accessed data in cheaper tiers.

**AWS IAM & Security**

11. **Explain IAM Roles, Policies, and Users. How do they interact?**

* **Users**: Individual accounts with credentials.
* **Roles**: Assigned temporary permissions for EC2, Lambda, etc.
* **Policies**: JSON documents defining permissions, attached to users, groups, or roles.

12. **How do you enforce least privilege access in AWS?**

* Use IAM policies with the principle of least privilege.
* Enable AWS Organizations SCPs for governance.
* Regularly audit IAM roles using IAM Access Analyzer.

13. **What are AWS KMS and Secrets Manager, and when should you use each?**

* **KMS (Key Management Service)**: Encrypts data at rest.
* **Secrets Manager**: Securely stores and rotates secrets like database credentials.

14. **How do you secure data at rest and in transit in AWS?**

* Use **AWS KMS** for encryption at rest.
* Use **TLS/SSL** for encryption in transit.
* Enable **S3 Bucket Encryption** and enforce policies.

15. **What steps would you take if you suspect an EC2 instance compromise?**

* Isolate instance by removing it from Security Groups.
* Capture logs and memory dump.
* Rotate compromised IAM credentials.
* Perform forensic analysis using AWS GuardDuty findings.

**AWS Deployment & Automation**

16. **What is Infrastructure as Code (IaC), and why is Terraform used over CloudFormation?**

* IaC automates resource provisioning.
* Terraform supports multiple clouds, has better modularity.

17. **How do you structure a Terraform project for a multi-environment setup?**

* Separate state files for dev, stage, prod.
* Use backend S3 with DynamoDB locking.
* Implement modules for reusable components.

18. **Explain AWS Systems Manager Parameter Store vs. Secrets Manager.**

* Parameter Store: Basic key-value storage.
* Secrets Manager: Secure secrets with automatic rotation.

19. **How would you automate EC2 instance patching in AWS?**

* Use AWS Systems Manager Patch Manager.
* Configure Maintenance Windows for patching.

20. **What is AWS CloudFormation Drift Detection, and how does it help?**

* Detects if manually changed infrastructure drifts from the IaC template.

---

This document continues with in-depth coverage of Containers & Kubernetes (EKS), Monitoring & Logging, AWS Serverless & Event-Driven Architectures, AWS Security Best Practices, AWS Cost Optimization & Performance, and AWS Troubleshooting & Best Practices. Let me know if you want specific topics expanded further.





