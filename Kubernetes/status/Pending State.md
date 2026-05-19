## Pending State (Kubernetes)

👉 **Meaning:** Pod is accepted by Kubernetes but not yet running  

A Pod remains in Pending state when it cannot transition to Running. This usually happens due to **scheduling issues or initialization delays**.

---

### 1. Scheduling Phase (Most Common)

The Kubernetes scheduler is unable to place the Pod on any node because no node satisfies the constraints defined in the Pod spec.

**Common reasons:**
- Insufficient CPU, memory, or ephemeral storage  
- Node selector or node affinity mismatch  
- Taints and tolerations not aligned  
- Topology constraints not satisfied  
- Node conditions (NotReady, DiskPressure, MemoryPressure)  

👉 Insight: The Pod is rejected by the scheduler, not due to cluster failure  

---

### 2. Post-Scheduling Phase (Scheduled but Not Running)

Even after a node is assigned, the Pod can remain Pending if initialization is not complete.

**Common reasons:**
- Image pull delays or failures  
- Init containers still running  
- Volume mount or PVC binding delays  
- Missing or delayed Secrets/ConfigMaps  

---

### 3. How to Debug

```bash
kubectl describe pod <pod-name>
```

Check:
- Events section (most important)  
- Scheduling errors vs initialization issues  
- Image pull / volume / config errors  

---

### 4. Key Insight

👉 In real production environments, most Pending Pods are caused by:
- Scheduling constraints  
- Misconfigurations  

Not infrastructure failures  

---

### 5. One-Line Summary

A Pod stays Pending either because no suitable node is available for scheduling, or because the assigned node cannot complete initialization successfully.
