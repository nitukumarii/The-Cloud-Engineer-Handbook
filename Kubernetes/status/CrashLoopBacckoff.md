## CrashLoopBackOff

👉 **Meaning:** Container is starting → crashing → restarting repeatedly  

CrashLoopBackOff occurs when a container repeatedly starts, crashes, and Kubernetes restarts it with an increasing backoff delay.

---

### Common Causes

- Configuration issues (missing environment variables, incorrect ConfigMaps/Secrets, wrong startup commands)  
- Probe misconfiguration (liveness/readiness probes too aggressive or incorrectly defined)  
- Resource constraints (low memory limits leading to OOMKilled)  
- Application failures (unhandled exceptions, startup failures)  
- External dependency issues (database/API connectivity failures)  

---

### Troubleshooting Steps

#### 1. Identify the failing pod
```bash
kubectl get pods
kubectl describe pod <pod-name>
```

Check:
- Restart Count  
- Container State (Error / OOMKilled)  
- Events section  

👉 Insight: Events often reveal issues like missing ConfigMaps or volume errors  

---

#### 2. Check logs (most critical step)
```bash
kubectl logs <pod-name> --previous
```

Check for:
- Missing environment variables  
- Application errors  
- Connection failures  

👉 Insight: Logs usually show the exact root cause  

---

#### 3. Validate configuration
- ConfigMaps and Secrets  
- Environment variables  
- Startup commands  

👉 In real scenarios, many issues are caused by misconfigured endpoints or missing values  

---

#### 4. Check probes
```bash
kubectl describe pod <pod-name>
```

Look for:
- Liveness/Readiness probe failures  
- Incorrect endpoints or timing  

👉 Insight: Misconfigured probes can cause unnecessary restarts  

---

#### 5. Check resource limits
```bash
kubectl describe pod <pod-name>
kubectl top pod <pod-name>
```

Check:
- Memory limits  
- OOMKilled events  

👉 Insight: Low memory limits can kill containers  

---

#### 6. Fix and redeploy

Apply fixes:
- Correct configuration  
- Adjust resource limits  
- Fix application or dependencies  

Monitor:
```bash
kubectl get pods -w
```

---

### SRE Perspective (Prevention)

- Standardize probe configurations  
- Define proper resource requests/limits  
- Improve observability (metrics, logs, alerts)  
- Create runbooks for recurring issues  
- Convert incidents into platform improvements  

---

### Key Takeaway

CrashLoopBackOff is usually a **symptom, not the root cause**.  

👉 Focus not only on fixing quickly, but preventing recurrence through better configuration, observability, and system design.
