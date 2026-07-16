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
