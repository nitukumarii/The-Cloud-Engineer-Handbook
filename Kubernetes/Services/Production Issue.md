# 📘 SRE Troubleshooting – Latency Issue in Kubernetes (EKS)

## ❓ Problem Statement

In a production environment running on Kubernetes (EKS), a latency spike is observed between 12–1 PM, leading to a P1 incident. The objective is to identify the root cause by analyzing application behavior, Kubernetes components, and backend dependencies in a structured way.

---

## ✅ End-to-End Troubleshooting Approach

In a real-world production scenario, when a latency issue occurs, my first step is to validate the issue using monitoring tools such as Splunk or APM dashboards. I analyze latency metrics across multiple layers, including API response time, backend processing time, and database query latency. This helps me identify where the delay is occurring. For example, if API latency is high but database latency is normal, I narrow the issue to the backend layer. If database query latency is high, then the database becomes the likely bottleneck. The key idea is to identify where the system is spending the most time.

Once I identify the impacted layer, I validate service-level communication inside Kubernetes to ensure connectivity is not the issue. I send a request to the service using its DNS name:

```bash
curl http://database-service
```

This confirms that the Kubernetes Service is reachable and correctly routing traffic to backend pods. Since Services abstract pod IPs, this step ensures that service discovery and routing are working correctly.

After confirming connectivity, I move to application-level debugging by checking logs of the affected pods:

```bash
kubectl logs <pod-name>
```

Here, I look for slow queries, timeout errors, retries, or thread blocking patterns, as these are common indicators of latency issues in distributed systems.

Next, I inspect pod health:

```bash
kubectl describe pod <pod-name>
```

Even though the issue is latency and not a complete outage, I check for restarts and OOMKilled events. Frequent restarts can cause cold starts, cache loss, and reduced capacity, which increases latency. Similarly, OOMKilled events indicate memory pressure, where the application slows down before being terminated and restarted.

I then verify liveness and readiness probes:

```bash
kubectl get pod <pod-name> -o yaml
```

If readiness probes are failing, fewer pods are available to serve traffic, increasing load on remaining pods and causing latency. Misconfigured liveness probes can lead to unnecessary restarts, further degrading performance.

Next, I check resource utilization:

```bash
kubectl top pod
```

High CPU usage, memory pressure, or throttling are common causes of latency due to resource contention, so this step helps identify performance bottlenecks.

I also validate service endpoints:

```bash
kubectl get endpoints
```

This ensures that the Service is routing traffic only to healthy pods and not to unhealthy or terminating instances.

If the issue still points to the database, I investigate database-level metrics such as slow queries, connection pool limits, locking issues, and disk I/O latency, as these directly impact response time.

Finally, I check infrastructure and node health:

```bash
kubectl get nodes
```

This helps identify node-level issues or network latency between pods, which can also contribute to overall system latency.

---

## 🔑 Key Insight

Even in latency scenarios, checking pod restarts and OOMKilled events is critical because they indicate resource instability. Restarts reduce available capacity and introduce cold starts, while memory pressure slows down applications before failure, both of which directly increase latency.

---

## 🎯 Conclusion

Latency troubleshooting in Kubernetes requires a systematic approach where monitoring data, logs, pod health, resource usage, and backend dependencies are correlated. The goal is to identify where time is being spent in the system and isolate the exact bottleneck rather than assuming a single point of failure.
