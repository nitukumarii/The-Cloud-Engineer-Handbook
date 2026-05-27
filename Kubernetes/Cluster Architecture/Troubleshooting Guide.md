# 📦 Kubernetes Pod YAML – Creation, Editing & Troubleshooting Guide

---

# 🧠 Overview

In Kubernetes, Pods are usually managed using YAML files.  
You should know:

- How to create YAML  
- How to edit it  
- How to fix errors  
- When to use each method  

---

# 🚀 1. Creating Pod YAML

## 🔹 Method 1: Manual (Using vi)

```bash
vi redis.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: redis
spec:
  containers:
  - name: redis
    image: redis123
```

```bash
kubectl apply -f redis.yaml
```

---

## 🔹 Method 2: Auto-Generate (Best Practice)

```bash
kubectl run redis --image=redis123 --restart=Never --dry-run=client -o yaml > redis.yaml
```

👉 Fast, safe, avoids syntax errors

---

# ✍️ 2. Editing YAML

## 🔹 Edit File

```bash
vi redis.yaml
```

### vi basics:

```
i       → insert mode
Esc     → exit insert
:wq     → save & exit
:q!     → exit without saving
```

---

## 🔹 Edit Live Resource

```bash
kubectl edit pod redis
```

👉 Opens YAML directly from cluster

---

# ⚠️ 3. Troubleshooting – Swap File Error

## ❌ Error:

```
E325: ATTENTION
Found a swap file ".redis.yaml.swp"
```

## 🔍 Cause:

- Previous edit crashed  
- File already open in another session  

---

## ✅ Solution (FASTEST)

Press:

```
E
```

👉 Edit anyway (safe in labs/exams)

---

## 🧹 Alternative Fix

```bash
rm -f .redis.yaml.swp
```

---

# 🔧 4. Fixing Wrong Image Issue

## ❌ Current:

```yaml
image: redis123
```

## ✅ Fix:

```yaml
image: redis
```

---

## ⚠️ Important

👉 Pods are mostly **immutable**

So after editing:

```bash
kubectl delete pod redis
kubectl apply -f redis.yaml
```

---

# ⚡ Alternative (Faster Way)

```bash
kubectl set image pod redis redis=redis
```

👉 Updates image without YAML

---

# 🧠 5. When to Use What

| Task | Command |
|------|--------|
| Create YAML fast | `kubectl run --dry-run -o yaml` |
| Write YAML manually | `vi file.yaml` |
| Apply YAML | `kubectl apply -f file.yaml` |
| Edit YAML file | `vi file.yaml` |
| Edit live Pod | `kubectl edit pod` |
| Fix image quickly | `kubectl set image` |
| Debug stuck Pod | `kubectl describe pod` |

---

# ⚠️ Common Mistakes

❌ Editing YAML but not reapplying  
❌ Forgetting Pods need recreation after changes  
❌ Panic on swap file error  
❌ Writing YAML from scratch in exams  

---

# 🎯 Interview Tips

👉 “Pods are immutable for fields like image, so we recreate them after updating YAML.”

👉 “I prefer generating YAML using `--dry-run` instead of writing from scratch.”

---

# 🧩 Final Mental Model

```
Create → run + dry-run + yaml  
Edit → vi or kubectl edit  
Fix → delete + apply  
Fast fix → kubectl set image  
```

---

# 🧠 Summary

- Use auto-generated YAML for speed  
- Use vi for editing  
- Handle swap file with "E"  
- Recreate Pod after changes  
- Use `set image` for quick fixes  
