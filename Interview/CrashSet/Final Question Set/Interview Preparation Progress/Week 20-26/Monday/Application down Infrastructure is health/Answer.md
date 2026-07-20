# Interview-Ready Answer (60–90 Seconds)

**Question:** *Infrastructure is healthy, but the application is failing. How do you troubleshoot it?*

> "If the infrastructure is healthy, my focus shifts to the application layer. First, I'd determine the scope of the issue by checking monitoring tools like **Prometheus, Grafana, Datadog, or Splunk** to understand whether the problem is affecting a single application instance or the entire service. I'd also review metrics such as **5xx error rates, response time, request volume, and recent alerts**.
>
> Based on that, my initial hypothesis would be an application configuration issue, a recent deployment, a dependency failure such as a database or external API, authentication issues, or an application bug.
>
> I would then review the **application logs** using tools like Splunk, Datadog Logs, or `journalctl` if it's running as a Linux service, to identify errors such as exceptions, connection failures, or timeout messages. Next, I'd verify whether there were any recent deployments or configuration changes and validate environment variables, configuration files, secrets, and certificates. If the application depends on a database, cache, or external API, I'd verify those dependencies are healthy and that the application can communicate with them successfully.
>
> Once I identify the root cause, I'd implement the appropriate fix, confirm that the application is healthy by monitoring logs and metrics, and finally document the RCA and improve monitoring or alerting to prevent similar incidents in the future."
