# 📌 Kubernetes ReplicaSet - Basics

---

## 🔹 What is a ReplicaSet?

A ReplicaSet ensures that a specified number of identical Pods are running at all times.

It maintains the desired state by creating or deleting Pods automatically.

---

## 🔹 Why do we use ReplicaSet?

- Maintain application availability
- Provide self-healing
- Ensure fixed number of Pods

---

## 🔹 Simple Working

- If Pods < desired → creates new Pods  
- If Pods > desired → deletes extra Pods  

---

## 🔹 Basic YAML Example

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
```

---

## 🔹 Basic Commands

```bash
kubectl get rs
kubectl describe rs <name>
kubectl scale rs <name> --replicas=5
Change the number of Pods in this ReplicaSet to 5
kubectl delete rs <name>
```

---

## 🎯 Summary

ReplicaSet ensures a fixed number of Pods are always running and replaces failed Pods automatically.
