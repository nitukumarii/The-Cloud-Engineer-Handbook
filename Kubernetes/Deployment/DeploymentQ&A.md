## 📚 Kubernetes Deployment – Interview Q&A

### 1. What is a Deployment in Kubernetes?

A Deployment is a Kubernetes object that manages Pods using ReplicaSets.

It provides:
- Scaling
- Rolling updates
- Rollbacks

👉 It allows you to define the desired state, and Kubernetes ensures that state is maintained automatically.

---

### 2. Difference between Deployment and ReplicaSet?

| Feature        | Deployment                     | ReplicaSet                |
|----------------|------------------------------|---------------------------|
| Purpose        | Manages application lifecycle | Maintains pod count       |
| Updates        | Supports rolling updates      | No update mechanism       |
| Rollback       | Supported                    | Not supported             |
| Usage          | Used in real-world scenarios | Rarely used directly      |
| Management     | Manages ReplicaSets          | Manages Pods              |

👉 Deployment sits above ReplicaSet.

---

### 3. Why do we use Deployment instead of ReplicaSet?

We use Deployment because it provides advanced features:

- Rolling updates (zero downtime)
- Rollbacks to previous versions
- Easy scaling
- Version control (revisions)

👉 ReplicaSet can only maintain pod count, but cannot manage updates.

---

### 4. What is `replicas` field?

The `replicas` field defines how many Pods should be running.

Example:
```yaml
replicas: 3
```

👉 Kubernetes ensures that exactly 3 Pods are always running.

---

### 5. What happens when replicas = 0?

```yaml
replicas: 0
```

👉 All Pods will be terminated.

- No Pods will be running
- Application becomes unavailable

👉 Useful for:
- Temporarily stopping an application
- Saving resources
