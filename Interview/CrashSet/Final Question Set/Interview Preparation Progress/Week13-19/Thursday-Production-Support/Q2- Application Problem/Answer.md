### How do you troubleshoot an application outage?



### 1. Confirm impact
      ↓
### 2. Check monitoring & alerts
      ↓
### 3. Check application health
      ↓
### 4. Check logs
      ↓
### 5. Check CPU/Memory/Disk
      ↓
### 6. Check Network/DNS/Load Balancer
      ↓
### 7. Check Database & Dependencies
      ↓
### 8. Restore service
      ↓
### 9. Monitor recovery
      ↓
### 10. RCA & Prevention



# How do you troubleshoot an application outage?

Whenever there's an application outage, I follow a systematic approach to identify the root cause while minimizing business impact.

## 1. Confirm the Scope and Impact

First, I determine the scope of the incident by checking whether it affects:
- A single user
- A specific service
- A region
- All users

I review monitoring dashboards and alerts using **Prometheus, Grafana, CloudWatch, or Splunk** to understand the impact by checking:
- Latency
- Error rates (4xx/5xx)
- Request volume
- Service availability
- CPU and Memory utilization

---

## 2. Verify Application Health

Next, I verify whether the application is running correctly.

I check:
- Pod status
- Restart count
- Events
- Application logs

```bash
kubectl get pods -n payment
kubectl describe pod <pod-name> -n payment
kubectl logs <pod-name> -n payment
```

If I find application errors or exceptions, I work with the application team to identify and resolve the issue.

---

## 3. Check Infrastructure Health

If the application appears healthy, I verify the underlying infrastructure to rule out resource exhaustion.

I check:
- CPU utilization
- Memory usage
- Disk space
- Network utilization

```bash
kubectl top pods
kubectl top nodes

top
free -m
df -h
```

---

## 4. Check Networking

If infrastructure is healthy, I investigate the networking layer.

I verify:
- Kubernetes Services
- Ingress
- AWS Load Balancer health
- DNS resolution
- Service-to-service connectivity

```bash
kubectl get svc
kubectl get ingress

nslookup <service>

curl <application-url>
```

---

## 5. Verify External Dependencies

If the application depends on external components, I verify that they are healthy and responding normally.

Examples include:
- Database
- Redis/Cache
- Message Queues (Kafka/RabbitMQ)
- External APIs
- Authentication services

---

## 6. Restore the Service

Once I identify the root cause, I restore the service as quickly as possible.

Depending on the issue, I may:
- Restart a failed service
- Roll back a deployment
- Scale the application
- Fix a configuration issue
- Work with the application team to resolve database or application-related problems

Throughout the incident, I keep stakeholders informed and continuously monitor the system until all metrics return to normal.

---

## 7. Perform Root Cause Analysis (RCA)

After the incident is resolved, I:
- Perform a Root Cause Analysis (RCA)
- Document the findings
- Update runbooks
- Improve monitoring and alerting
- Implement preventive measures to avoid similar incidents in the future
