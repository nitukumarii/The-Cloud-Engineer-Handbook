# Kubernetes Storage Flow (Pod → PVC → PV)

## Core Statement

The volume defined in a Pod is a **mount point and connector (bridge)** that allows a container to access storage through a PersistentVolumeClaim (PVC), which is bound to a PersistentVolume (PV) backed by real storage.

---

## Full Request Path

```
Container → Volume → PVC → PV → StorageClass → Storage Provider
```

---

## Component Breakdown

### 1. Container
- Runs the application
- Reads/writes data to a filesystem path (e.g. `/data`)
- Has no awareness of PVC, PV, or actual storage

---

### 2. Volume (Pod Spec)
- Defined in `.spec.volumes`
- Mounted using `.spec.containers[].volumeMounts`
- Acts as:
  - A **mount point inside the container**
  - A **bridge to storage via PVC**

Important:
- Volume itself does NOT store data
- It only connects the container to storage

---

### 3. PersistentVolumeClaim (PVC)
- A **request for storage**
- Specifies:
  - Storage size
  - Access mode
  - StorageClass

Example:
```yaml
resources:
  requests:
    storage: 10Gi
```

---

### 4. PersistentVolume (PV)
- The **actual provisioned storage**
- Can be:
  - Cloud disk (AWS EBS, GCP PD)
  - NFS share
  - Local disk

Key point:
- PVC binds to exactly one PV

---

### 5. StorageClass
- Defines how storage is provisioned
- Controls:
  - Storage type (SSD/HDD)
  - Provisioning behavior
- Enables dynamic provisioning

---

### 6. Storage Provider
- Actual storage backend outside Kubernetes
- Examples:
  - AWS, Azure, GCP
  - Ceph, NFS

---

## Read/Write Flow

### Write Path
```
App → Container → Volume → PVC → PV → Storage → Disk
```

### Read Path
```
Disk → Storage → PV → PVC → Volume → Container → App
```

---

## YAML Example (Pod + PVC)

### Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: app-pod
spec:
  containers:
    - name: app
      image: nginx
      volumeMounts:
        - name: data
          mountPath: /data
  volumes:
    - name: data
      persistentVolumeClaim:
        claimName: my-pvc
```

### PVC
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
```

---

## Key Concepts

- Containers do NOT directly access storage
- Volume = interface inside Pod
- PVC = storage request
- PV = actual storage
- StorageClass = provisioning rules

---

## Important Clarification

Incorrect:
```
Volume = storage
```

Correct:
```
Volume = mount point + connector to storage (via PVC)
```

---

## Types of Volumes

### Uses PVC
- persistentVolumeClaim

### Does NOT use PVC
- emptyDir
- configMap
- secret

---

## Analogy

| Kubernetes | Real World |
|-----------|----------|
| Volume | Faucet |
| PVC | Water request |
| PV | Pipe |
| Storage | Water source |

---

## Final Takeaway

A volume in a Pod does not store data itself. It provides a mounted path inside the container that connects to persistent storage through a PVC, which is bound to a PV backed by real storage.
