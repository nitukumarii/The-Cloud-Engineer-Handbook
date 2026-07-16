### Application is slow — how do you investigate? 



<img width="677" height="760" alt="image" src="https://github.com/user-attachments/assets/e4c79f93-c7a5-405e-8dae-ecaf783c2386" />


# How do you troubleshoot an application performance issue (slow application)?

If an application is running slowly, I follow a structured approach to identify the bottleneck and restore performance while minimizing business impact.

## 1. Check Monitoring and Understand the Impact

First, I check monitoring dashboards and alerts using tools like **Prometheus, Grafana, CloudWatch, or Splunk** to understand the scope of the issue.

I verify whether the slowness is affecting:

- A single user
- A specific service
- A specific region
- All users

I review key performance metrics such as:

- Response time / latency
- Error rates (4xx/5xx)
- Request volume
- Throughput
- CPU utilization
- Memory utilization
- Network latency

---

## 2. Check Application Health and Logs

Next, I investigate the application layer by checking application logs to identify:

- Exceptions
- Slow API calls
- Database query failures
- Timeout errors
- Application errors

In Kubernetes environments, I check:

```bash
kubectl get pods -n payment

kubectl describe pod <pod-name> -n payment

kubectl logs <pod-name> -n payment
```

I also verify:

- Pod restart count
- Container status
- Application response time

---

## 3. Check Infrastructure Resources

If there are no application errors, I check the infrastructure layer to identify resource bottlenecks.

I verify:

- CPU usage
- Memory consumption
- Disk I/O
- Disk space
- Network utilization

Commands:

```bash
kubectl top pods

kubectl top nodes

top

free -m

df -h

iostat
```

Examples:

- High CPU → application processing issue or increased traffic
- High memory → possible memory leak
- High disk I/O → storage bottleneck

---

## 4. Investigate Networking Layer

If infrastructure resources look normal, I investigate the networking components.

I check:

- Kubernetes Services
- Ingress configuration
- Load Balancer health
- DNS resolution
- Connectivity between services

Commands:

```bash
kubectl get svc

kubectl get ingress

nslookup <service>

curl -v <application-url>
```

---

## 5. Check External Dependencies

If the application depends on external components, I verify their health and performance.

I check:

- Database connectivity
- Slow database queries
- Connection pool usage
- Message queues (Kafka/RabbitMQ)
- Cache services like Redis
- Third-party API response time

---

## 6. Identify Root Cause and Restore Performance

Once I identify the bottleneck, I take corrective actions based on the issue.

Examples:

- Scale application instances if traffic is high
- Restart unhealthy services
- Optimize database queries
- Increase CPU/memory resources
- Fix application configuration issues
- Roll back recent changes if they caused performance degradation

---

## 7. Monitor Recovery and Prevent Recurrence

After resolving the issue, I continue monitoring:

- Application latency
- Error rates
- Request throughput
- Resource utilization

Once everything returns to normal, I perform a **Root Cause Analysis (RCA)**.

I document the findings, update runbooks, improve monitoring and alerting, and implement preventive actions to avoid similar performance issues in the future.
