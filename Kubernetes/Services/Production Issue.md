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


---

# 🔴 Scenario 2: User Not Reaching Correct Destination (S3 / Backup Link)

## ⭐ Situation
In a production environment, a user attempts to access old reports stored in S3 by clicking on a URL such as `https://backup`. However, instead of reaching the expected destination, the user is either redirected incorrectly or fails to connect to the relevant application or storage endpoint.

---

## ⭐ Task
As an SRE, the objective is to identify why the request is not reaching the correct destination and restore proper routing so users can access the required reports without disruption.

---

## ⭐ Action
I approach this issue by tracing the request flow end-to-end to identify where the misrouting occurs.

The first step is to validate DNS resolution to ensure the domain is pointing to the correct endpoint:

```bash
nslookup backup
dig backup
```

If DNS is correct, I move to the ingress or load balancer layer to verify routing rules. I check whether the host or path-based routing is correctly configured and not pointing to an incorrect backend.

Next, I validate whether the request is being redirected incorrectly by the application. This includes checking if the backend is returning an invalid or outdated redirect URL.

Since the reports are stored in S3, I also verify whether the URL being used is valid. In many cases, issues arise due to expired pre-signed URLs, incorrect bucket paths, or region mismatches. I confirm whether the S3 object exists and whether access permissions are correct.

Additionally, I check for TLS or domain mismatches that may cause incorrect routing or blocked connections.

Throughout this process, I focus on identifying where the request flow breaks:

```text
User → DNS → Load Balancer / Ingress → Application → S3
```

---

## ⭐ Result
The issue is typically resolved by correcting DNS entries, fixing ingress or load balancer routing rules, or updating invalid S3 URLs. Once fixed, users are able to access the reports successfully, restoring normal functionality. This is considered a production issue as it directly impacts user access and business operations.

---

# 🔴 Scenario 3: Service & Load Balancer Latency / Routing Issue

## ⭐ Situation
In a Kubernetes (EKS) production environment, users report intermittent latency and failures while accessing an application exposed through a Kubernetes Service and an external Load Balancer (ALB/NLB).

---

## ⭐ Task
The goal is to identify whether the issue lies in the Kubernetes Service, pod health, or load balancer configuration, and ensure traffic is routed efficiently to healthy application instances.

---

## ⭐ Action
I begin by validating the Kubernetes Service and its endpoints to ensure traffic is being routed correctly to active pods:

```bash
kubectl get svc
kubectl get endpoints
kubectl describe svc <service-name>
```

This helps confirm whether the Service is correctly mapped to healthy pods.

Next, I verify pod health and readiness to ensure only healthy pods are receiving traffic:

```bash
kubectl get pods -o wide
kubectl describe pod <pod-name>
kubectl logs <pod-name>
```

I check for restarts, OOMKilled events, and readiness probe failures, as these can lead to degraded performance and increased latency.

I then validate resource utilization to identify bottlenecks:

```bash
kubectl top pod
```

High CPU or memory usage can cause slow responses and must be addressed.

After that, I check the load balancer configuration, specifically target group health and listener rules, to ensure traffic is distributed only to healthy instances. Misconfigured health checks or port mismatches can lead to uneven traffic distribution or dropped requests.

Finally, I analyze whether traffic is unevenly distributed across pods or if scaling issues exist, which can overload certain instances and increase latency.

---

## ⭐ Result
The issue is typically resolved by correcting service-to-pod mappings, fixing readiness probe configurations, or updating load balancer health checks and routing rules. Once resolved, traffic is evenly distributed, and application latency returns to normal. This improves system reliability and ensures consistent user experience.

---

# 🎯 Key SRE Insight

In both scenarios, the critical approach is to trace the request flow and identify where the failure or delay is introduced:

```text
User → DNS → Load Balancer → Service → Pod → Dependency (S3 / DB)
```

Rather than checking components randomly, an SRE focuses on identifying the exact layer where the issue occurs and systematically eliminating non-impacting components.
