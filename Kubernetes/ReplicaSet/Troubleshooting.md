# 🔥 Kubernetes ReplicaSet - Troubleshooting

---

## 🔹 Debugging Mindset

For any issue:

```bash
kubectl describe rs <name>
kubectl describe pod <pod>
kubectl get events
```

👉 Always check **Events first**

---

## 🔥 Issue: Pod not created

```bash
kubectl describe rs <name>
```

Check:
- Selector mismatch
- Events

---

## 🔥 Issue: Selector mismatch

```bash
kubectl get pods --show-labels
```

- Labels must match selector

---

## 🔥 Issue: Too many Pods

Cause:
- ReplicaSet adopted existing Pods

---

## 🔥 Issue: Pods getting deleted

Cause:
- Replica count exceeded

---

## 🔥 Issue: Pod Pending

```bash
kubectl describe pod <pod>
```

Check:
- CPU/Memory
- Node availability
- PVC issues
- Taints

---

## 🔥 Issue: Wrong Pods managed

Cause:
- Incorrect selector

---

## 🔥 Issue: ReplicaSet not creating Pods

Check:
- API validation error
- Selector mismatch
- Resource shortage

---

## 🔥 Issue: Node failure

- Node down → Pods lost  
- ReplicaSet creates new Pods  
- Scheduler places on new node  

---

## 🔥 Events-Based Debugging Flow

```bash
kubectl describe rs
↓
kubectl describe pod
↓
kubectl describe node
```

---

## 🔹 Important Note

For Pending Pods:
👉 Logs are NOT useful  
👉 Events are MOST important  

---

## 🎯 Final Tip

Say in interview:

“For ReplicaSet issues, I rely heavily on describe and events to identify root cause.”
