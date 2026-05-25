


# 🚀 Kubernetes Deployment Notes

## 🧠 What is a Deployment?

A Deployment manages Pods using ReplicaSets.

### Provides:
- Scaling
- Rolling updates
- Rollbacks

You define desired state, Kubernetes maintains it automatically.

✅ Declarative → You say what you want, K8s ensures it

---

A Kubernetes Deployment manages pods that are:

Ephemeral (can be created/destroyed anytime)
Identical replicas
Not tied to persistent identity or storage

So:

Pods from a Deployment = stateless workloads



## 🔁 How Deployment Works

Deployment → ReplicaSet → Pods

- Deployment creates ReplicaSet  
- ReplicaSet creates Pods  
- On update → new ReplicaSet is created  

---

## 🧩 Basic Deployment YAML

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx-deployment
  labels:
    app: nginx

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
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

---

## 🔥 Important Fields Explained

### 🔹 metadata.name
- Name of Deployment  
- Used to name ReplicaSets & Pods  

### 🔹 replicas
- Number of Pods to run  
- Default = 1  

### 🔹 selector

```yaml
selector:
  matchLabels:
    app: nginx
```

- Defines which Pods are managed  
⚠️ Must match template labels  

### 🔹 template (Pod Template)

```yaml
template:
  metadata:
    labels:
      app: nginx
  spec:
    containers:
```

- Defines Pod configuration  
- Same as Pod YAML (without apiVersion/kind)  

---

## ⚠️ Golden Rules

- selector == template labels  
- selector is immutable  
- Don’t overlap selectors across controllers  

---

## 🔄 Deployment Use Cases

- Create Pods via ReplicaSet  
- Update application (image change)  
- Rollback to previous version  
- Scale application  
- Pause & resume updates  

---

## 🔄 Rolling Update (Default Strategy)

Updates Pods gradually.

Ensures:
- Minimum Pods always running  
- No downtime  

### Default values:
- maxUnavailable = 25%  
- maxSurge = 25%  

---

## 🔹 Strategy Example

```yaml
strategy:
  type: RollingUpdate
  rollingUpdate:
    maxUnavailable: 1
    maxSurge: 1
```

### Meaning:
- maxUnavailable → 1 pod can go down  
- maxSurge → 1 extra pod can be created  

---

## 🔁 Deployment Update

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1
```

### What happens:
- New ReplicaSet created  
- Old ReplicaSet scaled down  
- New Pods replace old ones gradually  

---

## 🔙 Rollback

```bash
kubectl rollout history deployment/nginx-deployment
kubectl rollout undo deployment/nginx-deployment
```

---

## 📈 Scaling

```bash
kubectl scale deployment/nginx-deployment --replicas=10
```

---

## ⏸ Pause & Resume

```bash
kubectl rollout pause deployment/nginx-deployment
kubectl rollout resume deployment/nginx-deployment
```

### When to use:
- Multiple updates together  
- Avoid repeated rollouts  
- Controlled deployment  

---

## 📊 Check Status

```bash
kubectl get deployments
kubectl describe deployment <name>
kubectl rollout status deployment/<name>
```

---

## 📌 Deployment States

### 1. Progressing
- Creating/updating ReplicaSet  
- Pods becoming ready  

### 2. Complete
- All Pods updated  
- All Pods available  
- No old ReplicaSets running  

### 3. Failed
- Image pull error  
- Readiness probe failure  
- Insufficient resources  

---

## ⚙️ Advanced Fields

### 🔹 progressDeadlineSeconds
- Time to wait before marking deployment failed  

### 🔹 minReadySeconds
- Pod must be ready for X seconds  

### 🔹 revisionHistoryLimit
- Number of old ReplicaSets to keep (default: 10)  

### 🔹 paused
- Stops rollout temporarily  

---

## 🧠 Key Concepts

### 🔹 Pod-template-hash
- Auto-generated label  
- Prevents ReplicaSet conflict  

### 🔹 Revision
- Created when Pod template changes  
- Not created when scaling  

---

## 🚨 Common Mistakes

- selector != labels  
- changing selector after creation  
- overlapping labels  
- editing ReplicaSet directly  

---

## ⚡ Quick Commands Cheat Sheet

```bash
kubectl apply -f deployment.yaml
kubectl get deployments
kubectl describe deployment <name>
kubectl rollout status deployment/<name>
kubectl rollout history deployment/<name>
kubectl rollout undo deployment/<name>
kubectl scale deployment/<name> --replicas=5
kubectl set image deployment/<name> <container>=<image>
```

---

## 🧠 One-Line Summary

Deployment = Automated Pod management with scaling, updates, and rollback
