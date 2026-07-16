### Describe a major production incident you handled ?


# Major Production Incident – API Outage Due to AWS Load Balancer Health Check Failure (STAR)

## Situation

In my previous project, I was supporting a customer-facing payment platform hosted on **AWS EKS Kubernetes infrastructure**. During peak business hours, our monitoring system (**Prometheus, Grafana, and CloudWatch**) triggered alerts for a sudden increase in API failures.

Shortly after, the application support team reported that users were unable to complete payment transactions. The impact was that payment APIs were returning errors, affecting transaction processing for multiple banking partners.

## Task

As the on-call **SRE**, my responsibility was to quickly identify the failure point, restore service availability, coordinate with application and cloud teams, and ensure the incident was properly documented.

## Action

I first checked our monitoring dashboards to understand the scope of the issue. I observed:

- API success rate had dropped significantly.
- HTTP 5xx errors were increasing.
- Kubernetes pods were running normally.
- CPU and memory utilization were within normal limits.

Since the application containers looked healthy, I moved my investigation to the networking layer.

I checked Kubernetes services and ingress configuration:

```bash
kubectl get svc -n payment

kubectl get ingress -n payment

kubectl describe ingress payment-ingress -n payment


```bash

I noticed that the AWS Application Load Balancer was marking some backend targets as unhealthy.

I then checked pod health status:

```bash

kubectl describe pod <pod-name> -n payment

```bash

I first ran kubectl describe pod, which showed repeated readiness probe timeout events. I then checked the application logs using kubectl logs 



kubectl logs payment-abc -n payment

```bash


and found that the /health endpoint was performing database and external dependency checks before returning a response. After discussing it with the application team, we confirmed that these dependency checks were causing the readiness probe to exceed the Load Balancer timeout.


Due to this, the load balancer removed healthy pods from rotation, leaving insufficient backend capacity to handle production traffic.

To restore service, I:

1. Increased application replicas to provide additional capacity.

```bash
kubectl scale deployment payment-service --replicas=10 -n payment

```

2. Temporarily adjusted load balancer health check timeout and interval settings.
3. Worked with the application team to optimize the readiness probe by removing unnecessary external dependency checks.
4. Monitored API success rate, latency, and transaction recovery through Grafana dashboards.


## Action

The root cause was an incorrectly configured Kubernetes readiness probe combined with aggressive AWS Load Balancer health check settings.

The application was healthy and capable of processing requests, but the health check configuration incorrectly marked instances as unavailable.



## Result

The incident was resolved within approximately 35 minutes with no data loss.

After the incident, we implemented improvements:

Improved Kubernetes readiness and liveness probe configurations.
Added alerts for unhealthy AWS Load Balancer targets.
Added production readiness checks before major changes.
Updated incident troubleshooting runbooks.
Improved monitoring coverage for application availability metrics.


