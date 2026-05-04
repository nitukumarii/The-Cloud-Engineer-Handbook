**Q: 🔹 Design a CI/CD Pipeline ?**
“In our project, developers worked on feature branches and pushed code to GitHub. When a pull request was created to merge into the main branch, a webhook 
triggered Jenkins. 
Jenkins then checked out the code, set up the environment, and executed the build process to compile the application and generate artifacts.”
After the build stage, we run security and quality scans such as static code analysis and dependency scanning. Then we package the application into a deployable 
artifact like a Docker image and push it to a registry. In the deployment phase, we release the application to environments using strategies like rolling or 
canary deployments, often via tools like Argo CD for Kubernetes.
Finally, we monitor the application using tools like Prometheus and Grafana to track performance, errors, and system health.”
<img width="323" height="480" alt="image" src="https://github.com/user-attachments/assets/377db755-9a57-474f-bd48-f5894740c7a1" />
<img width="458" height="702" alt="image" src="https://github.com/user-attachments/assets/c24ddcd1-4c66-461e-a553-265f0fcea010" />
<img width="445" height="713" alt="image" src="https://github.com/user-attachments/assets/961f6dfb-5f50-4ea4-ba47-40bb3030d406" />
<img width="403" height="178" alt="image" src="https://github.com/user-attachments/assets/2b78f23f-4fb9-4fe7-abab-c5ebadae9187" />


