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
# 🚀 Kubernetes Image Update – Pods vs Deployments

The `kubectl set image` command is used to update container images using the syntax: `kubectl set image <resource-type> <resource-name> <container-name>=<image-name>:<tag>`. For example, `kubectl set image deployment myapp nginx=nginx:1.25` updates the container image inside a Deployment.

---

## 🧠 1. If we need to change image of a running Pod → delete & recreate?

Yes, this is correct. Pods are mostly immutable, so you cannot reliably change the image of a running Pod. The correct approach is to delete the existing Pod and recreate it using an updated YAML file, for example: `kubectl delete pod redis` followed by `kubectl apply -f redis.yaml`.

---

## 🧠 2. Deleting a Pod won’t affect production?

This is wrong if the Pod is standalone. Deleting a standalone Pod will cause downtime because there is no controller to recreate it, so the application goes down. However, if the Pod is managed by a Deployment, ReplicaSet, or StatefulSet, then deleting the Pod is safe because Kubernetes will automatically create a new one, ensuring the application remains available.

---

## 🧠 3. set image won’t stop running Pod?

This is wrong for Pods but correct for Deployments. Using `kubectl set image` on a Pod is not reliable and may restart or fail the Pod. However, when used on a Deployment, Kubernetes performs a rolling update where old Pods are gradually replaced by new ones with the updated image. This ensures the application stays up with no downtime.

---

## 🔥 Final Understanding

Pods cannot be safely updated and usually require deletion and recreation, which may cause downtime if unmanaged. Deployments, on the other hand, support safe image updates using rolling updates without affecting application availability.

👉 Memory tip: Pod → recreate, Deployment → update.

---
