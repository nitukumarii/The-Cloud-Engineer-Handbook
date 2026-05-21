# 🚀 Kubernetes Controllers – Complete Comparison Notes

---

# 🧠 What are these?

These are Kubernetes **workload controllers** that manage Pods:

- ReplicaSet → maintains pod count
- Deployment → manages updates + ReplicaSets
- StatefulSet → manages stateful apps
- DaemonSet → runs pod on every node

---

# 🔥 Quick Comparison Table

| Feature        | ReplicaSet          | Deployment              | StatefulSet                | DaemonSet                  |
|---------------|--------------------|------------------------|----------------------------|----------------------------|
| Purpose       | Maintain pod count | Manage app lifecycle   | Stateful apps              | Run on all nodes           |
| Pods          | Identical          | Identical              | Unique (identity + storage)| One per node               |
| Updates       | ❌ No              | ✅ Rolling updates     | ✅ Ordered updates         | Limited                    |
| Rollback      | ❌ No              | ✅ Yes                 | ✅ Yes                     | ❌ No                      |
| Scaling       | ✅ Yes             | ✅ Yes                 | ✅ Yes (ordered)           | Auto (per node)            |
| Storage       | ❌ No              | ❌ No                  | ✅ Yes (PVC per pod)       | ❌ No                      |
| Use Case      | Basic scaling      | Web apps / APIs        | DB / Kafka                 | Logging / Monitoring       |

---

# 📦 1️⃣ ReplicaSet

## 🧠 Purpose:
Maintains a fixed number of Pods

---

## 🧩 YAML

```yaml
apiVersion: apps/v1
kind: ReplicaSet

metadata:
  name: my-rs

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

## ⚠️ Key Points

- Ensures pod count
- No update/rollback support
- Rarely used directly

---

# 🚀 2️⃣ Deployment

## 🧠 Purpose:
Manages ReplicaSets and provides updates

---

## 🧩 YAML

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: my-deploy

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
        image: nginx:1.14

  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
```

---

## ⚠️ Key Points

- Supports rolling updates
- Supports rollback
- Most commonly used

---

# 🧠 3️⃣ StatefulSet

## 🧠 Purpose:
Manages stateful applications

---

## 🧩 YAML

```yaml
apiVersion: apps/v1
kind: StatefulSet

metadata:
  name: my-sts

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

## ⚠️ Key Points

- Each pod has:
  - Fixed name (web-0, web-1)
  - Own storage
- Ordered creation/deletion
- Requires Headless Service

---

# 🖥 4️⃣ DaemonSet

## 🧠 Purpose:
Runs one Pod on every node

---

## 🧩 YAML

```yaml
apiVersion: apps/v1
kind: DaemonSet

metadata:
  name: my-daemon

spec:
  selector:
    matchLabels:
      app: monitor

  template:
    metadata:
      labels:
        app: monitor

    spec:
      containers:
      - name: monitor
        image: nginx
```

---

## ⚠️ Key Points

- One pod per node
- Automatically runs on new nodes
- Used for:
  - Logging agents
  - Monitoring tools

---

# 🔥 Real-World Use Cases

| Controller   | Example Use Case            |
|-------------|---------------------------|
| ReplicaSet  | Basic scaling (rare use)  |
| Deployment  | Web apps, APIs            |
| StatefulSet | Databases, Kafka          |
| DaemonSet   | Prometheus, Fluentd       |

---

# 🧠 Key Differences (Easy Memory)

- ReplicaSet → “Keep X pods running”
- Deployment → “Update app safely”
- StatefulSet → “Keep data + identity”
- DaemonSet → “Run everywhere”

---

# ⚡ One-Line Summary

ReplicaSet = scaling  
Deployment = scaling + updates  
StatefulSet = state + identity + storage  
DaemonSet = one pod per node  

---

# 🎯 Interview Gold Line

> Deployment is used for stateless apps, StatefulSet for stateful apps, DaemonSet for node-level services, and ReplicaSet is mainly used internally by Deployment to maintain pod count.
