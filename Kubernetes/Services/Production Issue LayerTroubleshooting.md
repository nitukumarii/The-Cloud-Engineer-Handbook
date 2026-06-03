# 📘 SRE Scenario – Analyzing Latency at Edge Layer in Production

## ❓ Question

In a live production environment running on Kubernetes (EKS), how do you analyze latency at the edge layer (DNS, Load Balancer, Ingress) without impacting running traffic?

---

## ⭐ Situation

In a production system, users report increased API latency during peak hours. The application is exposed via DNS and a Load Balancer (Ingress/ALB), and the system is fully live, handling real user traffic. Since this is a production environment, any debugging approach must be safe and should not introduce additional load or instability.

---

## ⭐ Task

As an SRE, the objective is to identify whether the latency is introduced at the edge layer (DNS resolution, load balancer, or ingress) while ensuring that production traffic is not disrupted. The goal is to isolate the layer where the delay occurs using safe and controlled methods.

---

## ⭐ Action

I start by leveraging existing observability tools such as Splunk, APM dashboards, or monitoring systems to analyze request latency without generating additional traffic. I review metrics like API response time, time to first byte (TTFB), and upstream vs downstream latency to understand whether the delay occurs before or after the request reaches the application.

Next, I analyze Load Balancer or Ingress metrics (such as AWS ALB metrics), including target response time, request count, and HTTP error rates. This helps determine whether the load balancer is introducing latency or waiting on backend services.

If further validation is required, I perform controlled and minimal-impact testing using a single request with detailed timing breakdown:

```bash
curl -w "\nDNS: %{time_namelookup}\nConnect: %{time_connect}\nTTFB: %{time_starttransfer}\nTotal: %{time_total}\n" -o /dev/null -s https://your-api
```

This allows me to measure DNS resolution time, TCP connection time, time to first byte, and total response time without affecting production load.

To further isolate the issue, I compare external and internal latency by executing a request from within the Kubernetes cluster:

```bash
kubectl exec -it <pod> -- curl http://service-name
```

If the request is fast internally but slow externally, it indicates that the issue lies in the edge layer (DNS, Load Balancer, or Ingress). If both are slow, the issue is likely within the application or downstream dependencies.

I also validate DNS resolution safely using:

```bash
nslookup your-domain
dig your-domain
```

This confirms whether the domain is resolving correctly without impacting the system.

Throughout the process, I correlate all observations across layers to identify exactly where latency is introduced instead of checking components randomly.

---

## ⭐ Result

By using observability data and controlled testing, I can safely identify whether latency originates at the DNS, Load Balancer, or Ingress layer without impacting live traffic. This approach ensures quick isolation of the issue while maintaining production stability. Once identified, appropriate fixes such as optimizing load balancer configuration, correcting DNS entries, or tuning ingress rules can be applied to restore normal performance.

---

## 🎯 Key Insight

In production, latency analysis at the edge layer is performed using observability-first and minimal-impact validation techniques. The focus is on identifying where time is being spent in the request lifecycle while ensuring zero disruption to live traffic.
