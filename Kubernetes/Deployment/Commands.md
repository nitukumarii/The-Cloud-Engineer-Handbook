

## 🔹 Commands (Very Important)

### Create deployment
```bash
kubectl apply -f deployment.yaml
```

### Get deployments
```bash
kubectl get deployments

<img width="690" height="83" alt="image" src="https://github.com/user-attachments/assets/7967dd5b-0545-4cce-ba45-57c6d92149cd" />

```

### Describe deployment
```bash
kubectl describe deployment <name>
```

### Scale deployment
```bash
kubectl scale deployment <name> --replicas=5
```

### Update image
```bash
kubectl set image deployment/<name> nginx=nginx:1.25
```

---

## 🔹 Rollback & History

### 10. What is rollout?

A rollout is the process of **updating Pods to a new version**.

---

### Check rollout status
```bash
kubectl rollout status deployment/<name>
```

---

### View history
```bash
kubectl rollout history deployment/<name>
```

---

### Rollback
```bash
kubectl rollout undo deployment/<name>
```

