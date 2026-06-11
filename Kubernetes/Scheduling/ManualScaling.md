# Kubernetes Manual Scheduling - Quick Notes

## Normal Scheduling Flow

```text
Pod Created
    ↓
Scheduler Finds Pod
    ↓
Selects Best Node
    ↓
Sets nodeName
    ↓
Pod Runs
```

Pods are normally created **without** a `nodeName`.

```yaml
spec:
  containers:
  - name: nginx
    image: nginx
```

The Scheduler automatically assigns a node.

---

# What If There Is No Scheduler?

```text
Pod Created
    ↓
Pending
    ↓
No Scheduler
    ↓
Still Pending
```

The Pod will never run until it is assigned to a node.

---

# Method 1: Manual Scheduling During Creation

Specify `nodeName` in the Pod manifest.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  nodeName: node01
  containers:
  - name: nginx
    image: nginx
```

### Result

```text
Pod → node01
```

---

# Method 2: Existing Pod Already Created

You cannot change:

```yaml
spec:
  nodeName: node01
```

after the Pod is created.

### Why?

```text
nodeName = Immutable
```

For an existing Pending Pod, use a **Binding Object** (same thing the Scheduler does internally).

---

# Scheduler Internals

```text
Scheduler
    ↓
Creates Binding Object
    ↓
Assigns Pod to Node
```

---

# Interview Questions

### What does the Scheduler do?

Finds Pods without `nodeName` and assigns them to the most suitable node.

### What happens if there is no Scheduler?

Pods remain in the **Pending** state.

### How do you manually schedule a Pod?

Add:

```yaml
spec:
  nodeName: node01
```

during Pod creation.

### Can you modify `nodeName` later?

No. It is immutable.

### How do you schedule an existing Pending Pod?

Create a **Binding Object** and send it to the Pod Binding API.

---

# CKA Exam Commands

List nodes:

```bash
kubectl get nodes
```

Check Pod's node:

```bash
kubectl get pods -o wide
```

View scheduling details:

```bash
kubectl describe pod <pod-name>
```

---

# Memory Trick

```text
No Scheduler?
│
├─ New Pod      → Use nodeName
│
└─ Existing Pod → Use Binding Object
```
