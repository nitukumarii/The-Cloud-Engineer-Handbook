# 🚀 Kubernetes StatefulSet – Complete Notes

---

## 🧠 What is a StatefulSet?

A StatefulSet is used to manage **stateful applications**.

### ✅ Provides:
- Stable identity (fixed pod name)
- Persistent storage
- Ordered deployment & scaling

👉 Declarative: You define desired state, Kubernetes maintains it

---

## 🔁 How StatefulSet Works

StatefulSet → Pods (with identity + storage)

- Pods are NOT interchangeable
- Each pod has its own identity

---

## 🔥 Key Features (VERY IMPORTANT)

### 🔹 Stable Pod Names

```
web-0
web-1
web-2
```

Format:
```
<StatefulSet-name>-<ordinal>
```

---

### 🔹 Stable Network Identity

```
web-0.nginx.default.svc.cluster.local
```

👉 Requires Headless Service

---

### 🔹 Persistent Storage

```
web-0 → volume-0
web-1 → volume-1
```

👉 Data persists even if pod restarts

---

### 🔹 Ordered Deployment

```
web-0 → web-1 → web-2
```

👉 Next pod starts only after previous is ready

---

### 🔹 Ordered Deletion

```
web-2 → web-1 → web-0
```

---

## 🧩 Basic StatefulSet YAML

```yaml
apiVersion: apps/v1
kind: StatefulSet

metadata:
  name: web

spec:
  serviceName: "nginx"
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

  volumeClaimTemplates:
  - metadata:
      name: data
    spec:
      accessModes: ["ReadWriteOnce"]
      resources:
        requests:
          storage: 1Gi
```

---

## ⚠️ MUST KNOW REQUIREMENTS

### 🔹 Headless Service (VERY IMPORTANT)

```yaml
clusterIP: None
```

👉 Required for DNS & identity

---

### 🔹 Selector Rule

```
selector == template labels
```

---

## 🔄 Pod Identity (CORE CONCEPT)

Each pod has:
- Unique name → web-0
- Unique storage
- Stable identity

👉 Even after restart:
```
web-0 → comes back as web-0 (same storage)
```

---

## 🔄 Scaling Behavior

### Scale Up:
```
web-0 → web-1 → web-2 → web-3
```

### Scale Down:
```
web-3 → web-2 → web-1
```

---

## 🔄 Update Strategies

### 🔹 RollingUpdate (Default)

- Updates pods one-by-one
- Order: highest → lowest

```
web-2 → web-1 → web-0
```

---

### 🔹 OnDelete

- No automatic update
- Must delete pods manually

---

## ⚡ Partition Update (Advanced)

```yaml
partition: 1
```

👉 Only updates pods with index ≥ 1

---

## 📦 Storage Behavior (VERY IMPORTANT)

- Volumes are NOT deleted automatically
- Even if:
  - Pod deleted ❌
  - StatefulSet deleted ❌

👉 Must delete PVC manually

---

## 🚨 Limitations

- Requires Headless Service
- Slower updates (ordered)
- Manual storage cleanup
- Rollouts can get stuck

---

## 🔥 When to Use StatefulSet?

Use for:
- Databases (MySQL, MongoDB)
- Kafka, Zookeeper
- Any app needing:
  - Stable identity
  - Persistent storage

---

## ❌ When NOT to Use

Use Deployment if:
- Stateless apps
- No storage needed
- No ordering required

---

## 🧠 Key Concepts

### 🔹 Ordinal Index
```
0, 1, 2...
```

---

### 🔹 ControllerRevision
- Stores history
- Used for rollback

---

### 🔹 Pod Labels
```
apps.kubernetes.io/pod-index
statefulset.kubernetes.io/pod-name
```

---

## 🔙 Rollback

```bash
kubectl rollout undo statefulset/web
```

---

## 📊 Debugging Commands

```bash
kubectl get pods
kubectl describe pod <pod>
kubectl logs <pod>
kubectl get pvc
```

---

# 🔥 KEY POINTS TO REMEMBER

- StatefulSet = stateful apps only
- Pods have fixed identity (name + storage)
- Ordered:
  - Create → 0 → N
  - Delete → N → 0
- Requires:
  - Headless Service
  - Persistent storage
- Volumes are NOT auto-deleted
- Updates are slow and ordered

---

## 🧠 One-Line Summary

StatefulSet = Deployment + Identity + Storage + Ordering
