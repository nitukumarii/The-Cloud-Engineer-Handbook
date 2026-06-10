### Can you introduce yourself?

Hi, I’m Nitu. I have around X years of experience in AWS, DevOps, and cloud infrastructure.

I started my career with HCL as an analyst where I worked on monitoring and alerting using CloudWatch, Azure Monitor, and ServiceNow. 
Later, I moved into a more technical role managing AWS infrastructure, automation using Bash, and handling incidents.

Currently, I work on infrastructure automation using Terraform, CI/CD pipelines using Jenkins, and containerization with Docker and Kubernetes (EKS). 
I also focus on security best practices, cost optimization, and performance monitoring using tools like Datadog and Prometheus.

I’m particularly interested in building scalable, secure, and automated cloud environments.


### Explain your AWS security experience.


I have hands-on experience securing AWS environments across IAM, network, and application layers.

I implemented IAM least privilege access, enforced MFA, and used roles instead of users. For network security, I configured Security Groups and NACLs with restricted access.

At the application level, I used AWS WAF to protect against OWASP attacks and enabled GuardDuty for threat detection. 
For data protection, I used KMS for encryption and Secrets Manager for storing credentials securely.



### Have you secured a web application yourself?”

Yes, in my previous project, I secured a web application hosted on AWS.

We implemented AWS WAF to block SQL injection and XSS attacks. API Gateway was secured using IAM authentication and throttling to prevent abuse.

Backend services were deployed in private subnets, and access was controlled via Security Groups and a bastion host. 
Sensitive credentials were stored in AWS Secrets Manager, and data was encrypted using KMS.

We also enabled AWS Shield for DDoS protection and monitored traffic using VPC Flow Logs.

### Explain a critical issue you resolved


I handled a high CPU utilization issue on an EC2 instance.

First, I checked system processes using top and identified abnormal load. Then I analyzed CloudWatch metrics and observed a spike in incoming requests.

Using VPC Flow Logs, I identified suspicious traffic from specific IP ranges. We blocked those IPs using AWS WAF and implemented rate limiting.

Additionally, we adjusted auto-scaling policies to handle traffic spikes, which restored system stability.


### How do you connect or secure multiple AWS regions?

To securely connect multiple AWS regions, we can use:

- Transit Gateway for centralized connectivity across multiple VPCs and regions
- VPC Peering for simple connections (not scalable)
- Site-to-Site VPN for encrypted communication
- Direct Connect for dedicated private connectivity

For security:
- Use IAM and SCPs for access control
- Encrypt traffic using TLS
- Enable AWS Shield and WAF
- Use Network Firewall for additional protection

This ensures secure and scalable multi-region architecture.


### What are Terraform modules?


Terraform modules are reusable components that help standardize infrastructure deployment.

In my projects, I created modules for VPC, EC2, and security groups, which allowed consistent deployments across environments.

We used S3 for remote state storage and DynamoDB for state locking to avoid conflicts in team environments.


### Terraform state file?\


Terraform state file tracks infrastructure changes and maps resources to configurations.

In production, we store it in S3 with versioning enabled and use DynamoDB for state locking to prevent concurrent updates.

This ensures consistency and avoids conflicts in team environments.

### Explain your CI/CD experienc

I have implemented CI/CD pipelines using Jenkins and AWS tools.

My pipeline included:
- Code checkout from Git
- Build and unit testing
- Security scanning using SonarQube
- Docker image build and push to registry
- Deployment to EKS using Helm

I also optimized pipelines using parallel execution and caching.


### How do you secure EKS?


For EKS security:

- Used IRSA (IAM Roles for Service Accounts)
- Applied Network Policies using Calico
- Enabled EBS encryption for volumes
- Used Secrets Manager for credentials
- Enabled image scanning in ECR
- Enforced Pod Security Standards to prevent privilege escalation

### RDS experience?


I have worked with RDS for provisioning and basic management.

I configured Multi-AZ for high availability and automated backups using AWS Backup.

I monitored performance using CloudWatch and Performance Insights. I am currently improving my knowledge in query optimization and tuning.


### Languages used?

I use Python and Bash for automation tasks.

Python is used for scripting, Lambda functions, and API integrations. Bash is used for deployment scripts.

I use YAML for Kubernetes manifests, Terraform, and CI/CD pipelines, and I am familiar with Groovy for Jenkins pipelines.


🚀 HOW TO REACH 100% SELECTION
✅ 1. Always give REAL examples
✅ 2. Never say “I need to learn” directly
✅ 3. Speak confidently (even if unsure)
✅ 4. Answer structure:
Problem → What I did → Tools used → Result
