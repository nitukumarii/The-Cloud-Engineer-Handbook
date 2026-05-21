kubectl apply -f deployment.yaml
kubectl get deployments
kubectl describe deployment <name>
kubectl rollout status deployment/<name>
kubectl rollout history deployment/<name>
kubectl rollout undo deployment/<name>
kubectl scale deployment/<name> --replicas=5
kubectl set image deployment/<name> <container>=<image>


## 🔹 Commands (Very Important)

### Create deployment
```bash
kubectl apply -f deployment.yaml
```

### Get deployments
```bash
kubectl get deployments
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

