Core Features Explained (VERY IMPORTANT)

---

### 1️⃣ Stable Pod Identity

Pods created like:

```
web-0
web-1
web-2
```

👉 Format:
```
<StatefulSet-name>-<number>
```

---

### 💡 Important Behavior

If pod crashes:

```
web-0 → deleted → recreated → still web-0
```

👉 Same name, same identity

---

### 2️⃣ Persistent Storage (VERY IMPORTANT)

Each Pod gets its own storage:

```
web-0 → volume-0
web-1 → volume-1
```

👉 Even if pod restarts:
- Data remains safe

---

### 3️⃣ Stable Network Identity

Each pod gets DNS name:

```
web-0.nginx.default.svc.cluster.local
```

👉 This allows:
- Pod-to-pod communication
- Database clustering

---

### ⚠️ Requires Headless Service

```yaml
clusterIP: None
```

👉 Without this → StatefulSet won't work properly

---

### 4️⃣ Ordered Pod Creation

Pods are created in sequence:

```
web-0 → web-1 → web-2
```

👉 Rule:
- Next pod starts only after previous is ready

---

### 5️⃣ Ordered Pod Deletion

Pods are deleted in reverse order:

```
web-2 → web-1 → web-0
```

---
