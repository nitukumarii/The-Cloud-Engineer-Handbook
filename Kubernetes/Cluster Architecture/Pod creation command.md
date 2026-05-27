# 📦 Kubernetes Pod Creation – Commands, Mistakes & Interview Notes

---

# 🚀 Creating Pod Using Image (Imperative Way)

## ✅ Command

```bash
kubectl run podname --image=imagename
```

### 🔹 Example

```bash
kubectl run nginx-pod --image=nginx
```

👉 Creates:
- Pod → nginx-pod  
- Container → nginx image  

---

## ⚠️ Force Pod Creation (Important)

```bash
kubectl run nginx-pod --image=nginx --restart=Never
```

👉 Ensures it creates a **Pod (not Deployment)**

---

# 📄 Creating Pod Using YAML (Declarative Way – Recommended)

## ✅ pod.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx
    image: nginx
```

---

## ▶️ Apply YAML

```bash
kubectl apply -f pod.yaml
```

---

# 🔍 Verify Pod

```bash
kubectl get pods
```

---

# ⚠️ Common Mistakes (VERY IMPORTANT)

❌ Wrong:
```bash
kubectl create -f podname --image=nginx
```

✔ Correct:
- `-f` is only for **files**
- Use `kubectl run` OR `kubectl apply -f`

---

❌ Thinking `kubectl run` always creates Pod  
✔ It may create Deployment in some cases → use:

```bash
--restart=Never
```

---

❌ Scaling by adding containers to same Pod  
✔ Always scale by **creating new Pods**

---

# 📌 Points to Remember

- Pod = smallest unit in Kubernetes  
- Usually **1 Pod = 1 Container**  
- Pods are **ephemeral**  
- Use YAML for production  
- `kubectl run` is for quick testing  
- Kubernetes does NOT run containers directly (uses Pods)  

---

# 🎯 Commonly Asked Interview Questions

---

## ❓ How do you create a Pod in Kubernetes?

> Using `kubectl run podname --image=imagename` or using a YAML file with `kubectl apply -f`.

---

## ❓ Difference between imperative and declarative?

- Imperative → `kubectl run`
- Declarative → YAML (`kubectl apply`)

---

## ❓ Why use YAML instead of command?

> YAML provides version control, reproducibility, and is used in production environments.

---

## ❓ Can a Pod have multiple containers?

> Yes, but mainly for sidecar/helper patterns.

---

## ❓ How do you scale Pods?

> By creating multiple Pods, not by adding containers to an existing Pod.

---

## ❓ Why use `--restart=Never`?

> To ensure `kubectl run` creates a Pod instead of a Deployment.

---

# 🧩 Final Mental Model

```
kubectl run → quick Pod
kubectl apply → production YAML
Pod → runs container
```

---

# 🧠 Summary

- Use `kubectl run` for quick Pod creation  
- Use YAML (`kubectl apply`) for real-world usage  
- Avoid common mistakes with `-f` and scaling  
- Understand Pod behavior for interviews  
