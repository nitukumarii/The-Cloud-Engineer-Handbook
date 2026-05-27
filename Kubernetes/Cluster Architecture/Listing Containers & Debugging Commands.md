# 🔍 Kubernetes – Listing Containers & Debugging Commands

---

# 🧠 Key Concept

👉 Kubernetes does NOT manage containers directly  
👉 Containers run inside **Pods**

---

# 📦 1. List Pods (Primary Command)

```bash
kubectl get pods
```

👉 Shows all running Pods  
👉 Each Pod contains one or more containers  

---

# 🔍 2. View Container Details Inside a Pod

```bash
kubectl describe pod podname
```

👉 Shows:
- Container names
- Images
- Status
- Events (errors, scheduling issues)
- Node info

---

# 📛 3. Get Container Names Only

```bash
kubectl get pod podname -o jsonpath='{.spec.containers[*].name}'
```

---

# 📄 4. View Container Logs

```bash
kubectl logs podname
```

👉 If multiple containers:

```bash
kubectl logs podname -c containername
```

---

# ⚙️ 5. Execute Command Inside Container

```bash
kubectl exec -it podname -- /bin/sh
```

👉 For multi-container Pods:

```bash
kubectl exec -it podname -c containername -- /bin/sh
```

---

# 🖥️ 6. Node-Level (Advanced – container runtime)

```bash
crictl ps
```

👉 Lists containers directly from runtime (containerd)

---

# ⚠️ Important Notes

- No direct `kubectl` command to list containers like Docker  
- Always interact via **Pods**  
- Use `describe`, `logs`, and `exec` for debugging  

---

# 🎯 Interview Answer

> Kubernetes does not provide a direct command to list containers because it manages Pods instead. To inspect containers, we use commands like `kubectl get pods`, `kubectl describe pod`, and `kubectl logs`.

---

# 🧩 Final Mental Model

```
Pod → contains container(s)
kubectl → works with Pods
crictl → works with containers (node level)
```

---

# 🧠 Summary

- Use `kubectl get pods` → list workloads  
- Use `kubectl describe pod` → inspect containers  
- Use `kubectl logs` → debug  
- Use `kubectl exec` → access container  
