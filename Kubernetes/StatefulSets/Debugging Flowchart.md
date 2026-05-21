# 🚀 StatefulSet Debugging Flowchart (Step-by-Step)

---

## 🧠 Goal

When StatefulSet is not working, follow this order:

👉 **Pod → Storage → Network → Application → Controller**

---

# 🔍 STEP 1: Check Pods (FIRST ALWAYS)

```bash
kubectl get pods
```

### 🧩 What to look for:

- Pending
- CrashLoopBackOff
- ImagePullBackOff
- Running but not Ready

---

## 👉 If Pod is NOT Running:

### 🔹 Describe pod

```bash
kubectl describe pod <pod-name>
```

### 🔹 Check logs

```bash
kubectl logs <pod-name>
```

---

# 🔍 STEP 2: Check Pod Order (StatefulSet Specific)

👉 StatefulSet creates pods in order:

```
web-0 → web-1 → web-2
```

### 🧩 Problem:

If:
```
web-0 ❌ (not ready)
```

👉 Then:
```
web-1, web-2 will NOT start
```

---

## ✅ Fix:

👉 Always fix **first pod (lowest index)** first

---

# 🔍 STEP 3: Check Storage (VERY IMPORTANT)

```bash
kubectl get pvc
```

### 🧩 Look for:

- Pending PVC ❌
- Not bound ❌

---

### 🔹 Describe PVC

```bash
kubectl describe pvc <pvc-name>
```

---

## 👉 Common Issues:

- No StorageClass
- No Persistent Volume
- Wrong access mode

---

# 🔍 STEP 4: Check Headless Service (Networking)

```bash
kubectl get svc
```

---

## 🧩 Verify:

- Service exists
- `clusterIP: None`

---

## ❌ If missing:

Pods cannot resolve each other

---

## 🔹 Test DNS

```bash
nslookup web-0.nginx
```

---

# 🔍 STEP 5: Check Application (Inside Container)

```bash
kubectl logs <pod-name>
```

---

## 🧩 Look for:

- App crash
- DB connection failure
- Missing environment variables

---

## ❌ Common Errors:

- CrashLoopBackOff
- Connection refused
- Config missing

---

# 🔍 STEP 6: Check Deployment / Update Status

```bash
kubectl rollout status statefulset/<name>
```

---

## 🧩 If stuck:

- Pod not ready
- Readiness probe failing

---

# 🔍 STEP 7: Check Events (FINAL STEP)

```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```

---

## 🧩 Helps identify:

- Scheduling issues
- Image pull issues
- Volume errors

---

# 🔥 COMPLETE FLOW (MEMORY)

```
1. Pods (status)
2. Pod order (web-0 first)
3. Storage (PVC)
4. Service (DNS)
5. Application logs
6. Rollout status
7. Events
```

---

# ⚡ QUICK DEBUG COMMAND SET

```bash
kubectl get pods
kubectl describe pod <pod>
kubectl logs <pod>
kubectl get pvc
kubectl describe pvc <pvc>
kubectl get svc
kubectl rollout status statefulset/<name>
kubectl get events
```

---

# 🧠 KEY DEBUGGING RULES

- Fix **web-0 first**
- Check **PVC before anything else**
- Check **logs for real error**
- StatefulSet = **order matters**

---

# 🎯 INTERVIEW GOLD LINE

> When debugging StatefulSet, I start with pod status, then check ordering constraints, verify storage (PVC), ensure headless service for networking, inspect logs for application issues, and finally check rollout status and events.

---
