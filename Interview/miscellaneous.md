1. Technical Interview Questions
A. Linux & Bash Scripting
Explain the difference between sed, awk, and grep.
How do you schedule a cron job to run every Monday at 3 AM?
Write a Bash script to check if a process is running and restart it if it's not.
What does set -e do in a Bash script?
How do you debug a Bash script?
What are nohup, screen, and tmux, and when would you use them?
How do you find and replace text in multiple files using Bash?
Explain ulimit and its impact on processes.
How do you check CPU and memory usage in Linux?
How do you find large files consuming disk space?
B. Kubernetes & Containerization
Explain the difference between a Deployment, StatefulSet, and DaemonSet in Kubernetes.
What is the purpose of a Kubernetes Ingress?
How does Kubernetes handle pod networking?
How do you scale a Kubernetes deployment manually and automatically?
What are Kubernetes ConfigMaps and Secrets? How do they differ?
How do you troubleshoot a failing Kubernetes pod?
Explain the role of the kube-proxy in Kubernetes.
How do you use kubectl to get logs of a specific pod container?
What is Helm, and how does it help in Kubernetes deployments?
How do you ensure high availability in a Kubernetes cluster?
C. CI/CD (Jenkins & GitLab CI/CD)
Explain how Jenkins pipelines work and their stages.
How do you set up a Jenkins pipeline using a Jenkinsfile?
What is the difference between Declarative and Scripted Jenkins pipelines?
How do you integrate GitLab CI/CD with Kubernetes?
What is a Jenkins agent, and how does it work?
How do you store and use secrets in a Jenkins pipeline?
How would you configure Jenkins to trigger a build automatically when code is pushed?
What are the differences between GitLab Runners and Jenkins Agents?
How do you handle rollback strategies in a CI/CD pipeline?
What are best practices for securing CI/CD pipelines?
D. Docker
What is the difference between a Docker container and a virtual machine?
How do you optimize a Docker image size?
What is the purpose of a .dockerignore file?
Explain the difference between CMD and ENTRYPOINT in Docker.
How do you troubleshoot a failing container?
How do you persist data in Docker?
Explain the difference between Docker Swarm and Kubernetes.
What happens when you run docker-compose up?
How do you limit CPU and memory usage for a Docker container?
How do you remove all stopped containers and unused images in Docker?
E. Ansible (Automation & Orchestration)
What are Ansible playbooks, roles, and inventories?
How do you write an Ansible playbook to install Apache on a server?
How do you test an Ansible playbook before applying changes?
Explain how Ansible Vault works for managing secrets.
What is the difference between command, shell, and raw modules in Ansible?
How do you use Ansible to manage multiple servers?
How do you handle idempotency in Ansible?
How does Ansible differ from Puppet and Chef?
How do you debug an Ansible playbook?
What is the purpose of ansible.cfg and .ansible.cfg?
F. AWS & Cloud (Bonus Skills)
What is the difference between an ELB and an ALB?
How does Auto Scaling work in AWS?
What are IAM roles and policies, and how do they differ?
How do you set up AWS CodePipeline for CI/CD?
What is the purpose of AWS Secrets Manager?
2. Behavioral Interview Questions
Can you describe a time when you had to troubleshoot a critical production issue?
Have you ever implemented automation that significantly improved efficiency?
Tell me about a conflict you faced while working in a DevOps team. How did you resolve it?
Can you share an experience where you worked under pressure to meet a deadline?
Describe a time when you had to deal with an unexpected infrastructure failure.
What’s the biggest mistake you’ve made in a DevOps role, and how did you fix it?
How do you prioritize multiple DevOps tasks when working on several projects?


1. Kubernetes Management

Q1: How do you manage and scale applications in Kubernetes?
➡ Talk about Horizontal Pod Autoscaler (HPA), Cluster Autoscaler, Ingress Controllers, and resource requests/limits.

Q2: What challenges have you faced while managing Kubernetes clusters, and how did you resolve them?
➡ Mention issues like pod scheduling failures, network policies, persistent storage, and high availability (HA) solutions.

Q3: Can you explain the role of Helm in Kubernetes?
➡ Helm is used for packaging, deploying, and managing Kubernetes applications via Helm charts.

2. CI/CD Pipelines (Jenkins, GitLab CI/CD)

Q4: How do you set up a CI/CD pipeline for a Kubernetes-based application?
➡ Use GitLab CI/CD or Jenkins with Docker, Helm, and Kubernetes to automate build, test, and deployment.

Q5: How do you ensure security in a CI/CD pipeline?
➡ Integrate tools like SonarQube (code quality), Trivy (container scanning), Snyk (dependency scanning), and enforce role-based access control (RBAC).

Q6: Have you worked with GitLab CI/CD? How does it compare to Jenkins?
➡ GitLab CI/CD is built-in and uses YAML, whereas Jenkins requires plugins and scripting. GitLab is more modern and scalable.

3. Configuration Management (Ansible)

Q7: How have you used Ansible for automation?
➡ Automated server provisioning, Kubernetes deployments, and app configurations using playbooks and roles.

Q8: Can you write a basic Ansible playbook to install Nginx?
➡ Example YAML playbook:

- name: Install Nginx
  hosts: web_servers
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present

Q9: How would you handle secret management in Ansible?
➡ Use Ansible Vault to encrypt sensitive data like API keys and passwords.

4. Monitoring & Troubleshooting

Q10: How do you monitor Kubernetes clusters?
➡ Use Prometheus + Grafana for metrics, and ELK or Loki for logging. Integrate with Datadog or AWS CloudWatch if required.

Q11: How do you troubleshoot a failing pod in Kubernetes?
➡ Run kubectl describe pod <pod-name> and kubectl logs <pod-name> to check errors, and use kubectl exec to investigate inside the pod.

Q12: How do you debug WordPress issues in a Linux environment?
➡ Check Apache/Nginx logs, MySQL database, WordPress debug mode, and ensure correct file permissions (chown -R www-data:www-data).

5. AWS Deployment & Management

Q13: How do you design a resilient AWS infrastructure?
➡ Use Multi-AZ deployments, Auto Scaling, Elastic Load Balancing (ALB/NLB), RDS Multi-AZ, and S3 for storage.

Q14: How would you deploy Kubernetes workloads on AWS?
➡ Use AWS EKS (managed Kubernetes), IAM roles, security groups, and integrate with AWS services like ALB, RDS, and S3.

Q15: How do you handle secrets in AWS?
➡ Use AWS Secrets Manager or Parameter Store to store and retrieve sensitive information securely.

6. Docker & Containerization

Q16: How do you optimize Docker images?
➡ Use multi-stage builds, minimize image layers, use .dockerignore, and prefer lightweight base images like alpine.

Q17: How do you troubleshoot a broken Docker container?
➡ Check logs (docker logs <container_id>), inspect processes (docker ps -a), and restart or recreate (docker restart <container_id>).

Q18: What is the difference between Docker Compose and Kubernetes?
➡ Docker Compose is for local multi-container applications, whereas Kubernetes is for orchestrating containers at scale.

7. Source Control Management & Best Practices

Q19: What Git branching strategy do you follow?
➡ Use GitFlow (feature, release, hotfix branches) or trunk-based development depending on the project.

Q20: How do you handle merge conflicts in Git?
➡ Use git merge or git rebase, manually resolve conflicts in affected files, and commit changes.

Q21: How do you enforce code quality in a repository?
➡ Use pre-commit hooks, linting (ESLint, Pylint), static code analysis (SonarQube), and peer code reviews.

8. Troubleshooting & Support (Level 3 Support)

Q22: Can you walk us through a critical production issue you resolved?
➡ Explain a high-severity incident, your troubleshooting process, and the resolution. Highlight minimizing downtime.

Q23: How do you ensure minimal downtime when deploying updates?
➡ Use blue-green deployments, rolling updates, and feature flags to avoid disruptions.

Q24: How do you handle a failed deployment in production?
➡ Check CI/CD logs, rollback to the previous stable version, and analyze root causes before redeploying.

9. Security & Compliance

Q25: How do you ensure security in a Kubernetes environment?
➡ Use Network Policies, RBAC, Pod Security Standards (PSS), and tools like Falco for runtime security.

Q26: How do you protect sensitive credentials in DevOps workflows?
➡ Use HashiCorp Vault, AWS Secrets Manager, or Kubernetes Secrets, and never hardcode credentials.

10. Soft Skills & Collaboration

Q27: Have you worked closely with developers to improve workflows?
➡ Mention CI/CD automation, performance tuning, and monitoring improvements for dev teams.

Q28: How do you handle a situation where a developer pushes a faulty deployment?
➡ Discuss rollback strategies, incident response, and ways to prevent future issues (e.g., automated testing, approvals).

Q29: How do you document your work in a DevOps environment?
➡ Maintain README files, Confluence/Wiki documentation, Terraform code comments, and architecture diagrams.

Bonus: Scenario-Based Questions

These questions test your problem-solving ability and practical experience.

🔹 "Your Kubernetes pod keeps crashing due to an OOMKilled error. How would you fix it?"
➡ Adjust resource limits, check memory consumption, and optimize application memory usage.

🔹 "Your CI/CD pipeline is slow. How do you improve it?"
➡ Parallelize jobs, optimize test cases, use caching (e.g., Docker layer caching, dependency caching).

🔹 "A WordPress site on AWS EC2 is loading slowly. How do you troubleshoot?"
➡ Check server CPU/RAM, database performance, caching layers, CDN, and logs for bottlenecks.

Technical Questions
AWS Services
Explain how you would ensure high availability and fault tolerance for applications running on AWS.
What is the difference between Amazon S3 and Amazon EFS, and when would you use each?
How do you secure data in transit and at rest in AWS?
Describe how you’ve used VPC and its associated components (subnets, NAT gateways, route tables) to design a secure network in AWS.
How would you monitor and troubleshoot performance issues in an EC2 instance?
Automation and Scripting
Walk me through how you would use Python or Bash to automate a routine DevOps task.
How have you implemented Infrastructure as Code (IaC) in your previous roles? Which tools did you use, and why?
Can you write a script to automate the deployment of a simple web application to AWS using Terraform?
Describe how you have used Jenkins or a similar tool to create CI/CD pipelines.
What are the key considerations when automating the deployment of microservices using Kubernetes?
Containerization and Orchestration
How do Kubernetes Helm charts help with application deployment? Provide an example from your experience.
Explain the differences between Docker Compose and Kubernetes. When would you choose one over the other?
How have you used Prometheus and Grafana for monitoring in a Kubernetes environment?
What are Kubernetes namespaces, and how do they improve multi-tenancy in a cluster?
How do you secure containerized applications in a Kubernetes environment?
Performance and Incident Management
How do you approach root cause analysis for a production incident?
Explain a time when you used performance tuning techniques to optimize application performance.
Describe how you set up alerts and dashboards to monitor system health proactively.
What is your process for resolving high-priority incidents?
How do you handle resource contention in a highly utilized cloud environment?
Networking
How do you troubleshoot connectivity issues in a cloud environment (e.g., between EC2 instances or across VPCs)?
Describe how you would set up a secure VPN connection between an on-premise data center and AWS.
What are VPC endpoints, and when would you use them?
Security
What best practices do you follow to secure AWS environments?
Explain the concept of IAM roles and policies and how you have implemented them in your projects.
How do you handle security patching for cloud-based systems?
What is AWS GuardDuty, and how have you used it in your projects?
AWS Sovereign Cloud (ESC)
What challenges do you foresee in setting up a high-availability AWS ESC for European customers?
How would you ensure compliance with data sovereignty regulations while operating in a multi-region setup?
Behavioral Questions
Amazon Leadership Principles
Customer Obsession: Describe a time when you worked backwards from customer needs to solve a problem.
Ownership: Share an example where you went beyond your responsibilities to ensure project success.
Invent and Simplify: Tell me about a time when you simplified a complex process or introduced an innovative solution.
Are Right, A Lot: Describe a situation where you made a decision based on incomplete data. How did it turn out?
Learn and Be Curious: How have you invested in learning new technologies or skills to improve your performance at work?
Problem-Solving and Teamwork
Tell me about a time you resolved a conflict within your team.
Share an example of a project where you had to collaborate with multiple teams to achieve success.
Describe a situation where you identified a bottleneck in your workflow and how you addressed it.
How do you prioritize your tasks when you have multiple high-priority assignments?
Share an instance when you failed to meet a deadline. What did you learn from it?
Time Management and Pressure Handling
How do you manage stress when handling multiple on-call incidents?
Tell me about a time when you had to deliver results under tight deadlines. How did you manage it?
How do you ensure work-life balance while participating in 24x7 on-call rotations?
Mentorship and Leadership
Describe a time you mentored a junior team member. What was the outcome?
How have you handled disagreements with your manager or a senior team member?
How do you ensure proper documentation for your DevOps processes?
How do you handle a situation where developers push insecure code into production?
What’s your approach to continuously learning new DevOps tools and technologies?
