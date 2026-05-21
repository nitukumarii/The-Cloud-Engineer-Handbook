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


## 📚 Kubernetes Deployment – Advanced Q&A

---

## 🔹 Selector & Template

### 1. Why must selector match template labels?

The selector tells the Deployment which Pods to manage.

👉 It must match template labels so the Deployment can correctly identify and control its Pods.

---

### 2. What happens if they don’t match?

- Deployment will not manage the Pods it creates
- Pods may remain unmanaged (orphaned)
- Kubernetes may throw validation error

👉 Result: Broken Deployment

---

### 3. Can you change selector after creation?

❌ No

- Selector is **immutable**
- To change it → delete and recreate Deployment

---

### 4. What is the role of template section?

The `template` defines **how Pods should be created**.

It contains:
- Labels
- Container specs
- Environment, ports, etc.

👉 It acts as a **blueprint for Pods**

---

### 5. Where are containers defined?

Inside:

```yaml
spec:
  template:
    spec:
      containers:
```

---

## 🔹 Rolling Updates

### 6. What is RollingUpdate strategy?

A strategy that updates Pods **gradually** instead of all at once.

👉 Ensures:
- No downtime
- Continuous availability

---

### 7. Difference between maxSurge and maxUnavailable?

| Field           | Meaning |
|----------------|--------|
| maxSurge        | Extra Pods allowed during update |
| maxUnavailable  | Pods allowed to be down |

👉 Example:
- maxSurge = 1 → can create 1 extra Pod
- maxUnavailable = 1 → 1 Pod can be unavailable

---

### 8. What is Recreate strategy?

- Deletes all old Pods first
- Then creates new Pods

❌ Causes downtime  
✅ Simple but risky

---

### 9. How does zero downtime work?

- New Pods are created before deleting old ones
- Traffic is always served by running Pods

👉 Achieved using:
- RollingUpdate
- maxSurge & maxUnavailable

---


---

## 🔹 Advanced

### 11. What is revision in Deployment?

- A version of Deployment created during updates
- Each change in Pod template = new revision

---

### 12. How Deployment manages ReplicaSets?

- Creates new ReplicaSet on update
- Scales up new ReplicaSet
- Scales down old ReplicaSet

---

### 13. What happens during image update?

- New ReplicaSet is created with new image
- New Pods are created
- Old Pods are gradually deleted

---

### 14. What is crash loop and how Deployment handles it?

CrashLoopBackOff:
- Pod starts → crashes → restarts repeatedly

Deployment handling:
- Keeps trying to maintain desired replicas
- May result in repeated failures if issue not fixed

---

### 15. Difference between liveness and readiness probe?

| Probe Type       | Purpose |
|-----------------|--------|
| Liveness Probe   | Checks if container is alive |
| Readiness Probe  | Checks if container is ready to serve traffic |

👉 Key difference:
- Liveness failure → container restarted
- Readiness failure → traffic stopped (but container not restarted)

---

## 🧠 One-Line Summary

Deployment automates Pod lifecycle with updates, scaling, and rollback.
