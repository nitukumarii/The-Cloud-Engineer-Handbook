**Q: 🔹 Design a CI/CD Pipeline ?**


“In our project, developers worked on feature branches and pushed code to GitHub. When a pull request was created to merge into the main branch, a webhook 
triggered Jenkins. 
Jenkins then checked out the code, set up the environment, and executed the build process to compile the application and generate artifacts.”
After the build stage, we run security and quality scans such as static code analysis and dependency scanning. Then we package the application into a deployable 
artifact like a Docker image and push it to a registry. In the deployment phase, we release the application to environments using strategies like rolling or 
canary deployments, often via tools like Argo CD for Kubernetes.
We use Terraform when there are infrastructure-level changes such as creating or modifying cloud resources like VPCs, Kubernetes clusters, load balancers, or databases. If the change is only in application code, Terraform is not required.”
Finally, we monitor the application using tools like Prometheus and Grafana to track performance, errors, and system health.”
<img width="323" height="480" alt="image" src="https://github.com/user-attachments/assets/377db755-9a57-474f-bd48-f5894740c7a1" /> <img width="458" height="702" alt="image" src="https://github.com/user-attachments/assets/c24ddcd1-4c66-461e-a553-265f0fcea010" />
<img width="445" height="713" alt="image" src="https://github.com/user-attachments/assets/961f6dfb-5f50-4ea4-ba47-40bb3030d406" /> <img width="403" height="178" alt="image" src="https://github.com/user-attachments/assets/2b78f23f-4fb9-4fe7-abab-c5ebadae9187" />


1. Creating Kubernetes cluster
New environment (dev/staging/prod)
Provisioning Amazon EKS

👉 Terraform creates:

VPC
Subnets
Node groups
IAM roles
🟢 2. Scaling infrastructure
Increase node count
Add autoscaling

👉 Example:

Update node group size in Terraform
🟢 3. Adding Load Balancer / Ingress infra
Exposing app to internet

👉 Terraform creates:

ALB / NLB
Security groups
🟢 4. Database changes
New DB instance
Change instance size

👉 Example:

Upgrade RDS from t3.medium → t3.large
🟢 5. Networking changes
Add new subnet
Modify routing
VPC peering
🟢 6. Security changes
IAM roles
Policies
Security groups
🟢 7. Multi-environment setup
Creating staging or prod identical to dev
