## OOMKilled vs Pod Eviction (Kubernetes)

### 1. OOMKilled (Container-Level)
- Occurs when a container exceeds its memory limit  
- Triggered by the Linux kernel (OOM killer)  
- Only the specific container is terminated, not the entire pod  
- Kubernetes may restart the container, which can lead to CrashLoopBackOff  

**Common indicators:**
- Reason: OOMKilled  
- Exit Code: 137  

---

### 2. Pod Eviction (Pod-Level)
- Occurs when a node is under memory pressure  
- Triggered by the Kubelet  
- Entire pod is terminated and removed from the node  

**Pod status:**
- Status: Failed  
- Reason: Evicted  

---

### 3. Why Eviction Happens Before OOM
- Kubernetes does not allow pods to use full node memory  
- It reserves memory using:
  - kube-reserved (for system daemons)  
  - system-reserved (for OS)  
  - eviction-threshold (safety buffer)  
- If total pod memory exceeds allocatable memory, Kubelet evicts pods proactively  

---

### 4. Key Scenarios

**Slow Memory Increase**
- Kubelet detects pressure in time  
- Pods are evicted  

**Sudden Memory Spike**
- Kubelet cannot react quickly  
- Kernel kills container  
- Results in OOMKilled  

---

### 5. Key Difference Summary

**OOMKilled**
- Container-level  
- Reactive  
- Triggered by kernel  

**Evicted**
- Pod-level  
- Proactive  
- Triggered by Kubelet  

---

### 6. Interview-Ready Line

OOMKilled happens when a container exceeds its memory limit and is terminated by the Linux kernel, affecting only that container. In contrast, pod eviction is triggered by the Kubelet when the node is under memory pressure, and it removes entire pods proactively to protect node stability.
