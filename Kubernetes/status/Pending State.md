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

# 🚀 Kubernetes Troubleshooting: Pod in Pending State

## 📌 Problem
Pod is stuck in **Pending** state and not getting scheduled.  
Logs are **not available** because the container has not started yet.

---

## 🔍 Step-by-Step Troubleshooting

### 🔥 Step 1: Describe the Pod (MOST IMPORTANT)

```bash
kubectl describe pod <pod-name>
```

👉 Check the **Events section** at the bottom

You may see errors like:

```
0/3 nodes are available
Insufficient CPU
node(s) had taint
PersistentVolumeClaim not bound
```

💡 This step alone helps identify ~80% of Pending issues

---

### 🔥 Step 2: Check Node Status

```bash
kubectl get nodes
kubectl describe node <node-name>
```

👉 Look for:
- Node in `NotReady` state  
- Resource pressure (CPU/Memory)  
- Taints applied on nodes  

---

### 🔥 Step 3: Check Resource Requests

```bash
kubectl get pod <pod-name> -o yaml
```

👉 Verify:
- CPU / Memory requests too high  
- Scheduler unable to place pod  

---

### 🔥 Step 4: Check PVC (if used)

```bash
kubectl get pvc
kubectl describe pvc <pvc-name>
```

👉 Common issue:
- PVC is in `Pending` → Pod also remains `Pending`

---

### 🔥 Step 5: Check Taints & Tolerations

```bash
kubectl describe node
```

👉 If node has taint like:

```
NoSchedule
```

👉 Then pod must have matching **toleration**

---

### 🔥 Step 6: Check Scheduler Logs (Advanced)

```bash
kubectl logs -n kube-system kube-scheduler-<node>
```

👉 Use only if issue is still unclear

---

## ⚠️ Common Root Causes

- No nodes available for scheduling  
- Insufficient CPU/Memory  
- Node taints not tolerated by pod  
- PVC not bound  
- Resource requests too high  

---

## 🧠 Troubleshooting Flow

```
Pod Pending
   ↓
kubectl describe pod
   ↓
Check Events
   ↓
Node / Resource / PVC issue identified
   ↓
Fix root cause
```

---

## 🎯 Perfect Interview Answer

> “If a pod is in Pending state, logs won’t be available. First, I check `kubectl describe pod` to analyze events. Then I verify node availability and resources using `kubectl get/describe nodes`. I also check resource constraints, taints/tolerations, and PVC binding issues. Based on events, I identify the root cause.”

---

## 💡 Quick Mapping

| Problem                | Where to Check          |
|-----------------------|------------------------|
| No nodes available    | describe pod (events)  |
| Resource issue        | describe node          |
| PVC issue             | get/describe pvc       |
| Taints issue          | describe node          |
| Scheduling issue      | Events section         |

---

## 🔥 Pro Tip

> “For Pending pods, events are more useful than logs.”

### 4. Key Insight

👉 In real production environments, most Pending Pods are caused by:
- Scheduling constraints  
- Misconfigurations  

Not infrastructure failures  

---

### 5. One-Line Summary

A Pod stays Pending either because no suitable node is available for scheduling, or because the assigned node cannot complete initialization successfully.
