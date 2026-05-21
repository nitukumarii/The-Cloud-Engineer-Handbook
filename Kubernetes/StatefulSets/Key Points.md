## 🔥 When to Use StatefulSet?

Use when application needs:

- Database (MySQL, PostgreSQL)
- Kafka
- Zookeeper
- Any system needing:
  - Persistent data
  - Stable identity

---

## ❌ When NOT to Use

Use Deployment if:

- Stateless app
- No storage required
- No ordering needed

---

## 🧠 Key Concepts

---

### 🔹 Ordinal Index

```
0, 1, 2...
```

Used for:
- Pod naming
- Ordering

---

### 🔹 ControllerRevision

- Stores update history
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

- StatefulSet = stateful applications
- Pods have:
  - Fixed name
  - Fixed storage
  - Fixed identity
- Ordered:
  - Create → 0 → N
  - Delete → N → 0
- Requires:
  - Headless Service
  - Persistent storage
- Volumes are NOT auto-deleted
- Updates are slow and controlled
