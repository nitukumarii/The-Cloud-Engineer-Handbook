# Handling Failed Production Deployment

We performed production deployments through the approved change management process.

Before deployment, I validated the required approvals, dependencies, deployment plan, maintenance window, and rollback plan to ensure minimum impact on the production environment.

During deployment, we monitored application health and availability. If the deployment failed or introduced any issue, we immediately followed the rollback plan and restored the previous stable version to bring the application back as quickly as possible.

After rollback, we validated the application health, logs, and transaction flow to ensure the service was stable.

Once the issue was analyzed, we created a new deployment plan, reviewed it with the team, and scheduled another approved maintenance window for the next deployment attempt.
