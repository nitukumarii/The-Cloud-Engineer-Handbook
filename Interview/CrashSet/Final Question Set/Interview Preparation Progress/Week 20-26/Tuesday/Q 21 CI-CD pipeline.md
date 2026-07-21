
# Explain your CI/CD Pipeline

In my project, whenever a developer pushed code changes to Git, a webhook triggered the CI pipeline by sending an HTTP request to Jenkins.

Jenkins was used as the CI tool, where it performed steps like code checkout, build, unit testing, and generating application artifacts.
We also integrated SonarQube for code quality and security scanning.

After successful validation, Jenkins built the Docker image containing the application and required dependencies, and pushed the image to the container registry.

For continuous deployment, we used ArgoCD following GitOps principles to deploy the application into the AWS EKS cluster.

Along with application deployment, Terraform was used separately for provisioning and managing AWS infrastructure resources.

I have also worked with GitHub Actions in my recent project and used GitLab CI/CD in my personal projects.
