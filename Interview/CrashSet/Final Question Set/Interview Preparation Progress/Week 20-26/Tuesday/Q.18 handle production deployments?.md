# How do you handle production deployments?

Whenever there is a new feature update, the code changes are first pushed to Git and a pull request is raised for review. After approval from the team members, the changes are merged into the main branch.

For production deployment, we follow the change management process. Before deployment, we verify the required approvals, dependencies, deployment plan, and rollback plan.

During the deployment, I monitor the application health, Kubernetes cluster health, pod status, and node health to ensure the deployment is progressing correctly.

After deployment, I use observability tools like Dynatrace and Splunk to monitor application logs, error rates, response time, and transaction flow to confirm that there are no issues introduced by the deployment.

If any issue occurs, we follow the rollback procedure to restore the previous stable version.

The main objective of production deployment is to release changes safely while maintaining application availability and minimizing downtime.
