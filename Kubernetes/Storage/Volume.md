# Kubernetes Volumes (Complete Storage Notes)

## Core Concept

Volumes are the most primitive storage abstraction in Kubernetes.

- Defined inside a Pod spec
- Mounted into one or more containers
- Provide a filesystem path inside the container

👉 Important:
- Volumes do NOT store data themselves
- They act as a **mount point + connector to storage**

---

## Volume Lifecycle

- Tied to the Pod lifecycle
- When the Pod is deleted → volume is deleted

Exception:
- If volume connects to persistent storage (via PVC), data survives

---

## Types of Volumes

### 1. Ephemeral Volumes

These exist only for the lifetime of the Pod.

---

### emptyDir

- Created when Pod starts
- Deleted when Pod stops

Use cases:
- Cache
- Scratch space
- Sharing data between containers

#### Memory-backed emptyDir

```yaml
emptyDir:
  medium: Memory
```

- Uses RAM (tmpfs)
- Faster
- Counts against container memory

---

### configMap

- Inject configuration as files
- Read-only

---

### secret

- Inject sensitive data
- Stored as base64 (NOT encrypted by default)
- Mounted as files

---

### projected

- Combines multiple sources:
  - configMap
  - secret
  - downwardAPI
  - serviceAccountToken

---

### hostPath ⚠️

- Mounts node filesystem into Pod

Risks:
- Breaks portability
- Node-dependent
- Security risk (container escape)

👉 Avoid in production

---

## Ephemeral Volume Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: shared-data-example
spec:
  containers:
  - name: writer
    image: busybox
    command: ["sh", "-c", "echo hello > /data/msg && sleep 3600"]
    volumeMounts:
    - mountPath: /data
      name: shared

  - name: reader
    image: busybox
    command: ["sh", "-c", "cat /data/msg && sleep 3600"]
    volumeMounts:
    - mountPath: /data
      name: shared

  volumes:
  - name: shared
    emptyDir: {}
```

Pattern:
- Writer writes data
- Reader reads data
- Common in sidecar pattern

---

## 2. Persistent Storage via Volumes

Some volume types connect to persistent storage using PVC.

---

### persistentVolumeClaim (Volume Type)

```yaml
volumes:
  - name: data
    persistentVolumeClaim:
      claimName: my-pvc
```

👉 This volume:
- Does NOT store data
- Connects Pod → PVC → storage

---

## Persistent Storage Architecture

```
Container → Volume → PVC → PV → StorageClass → Storage Provider
```

---

## 3. PersistentVolumeClaim (PVC)

PVC is a **request for storage**.

Defines:
- Size
- Access mode
- StorageClass

---

### PVC Example

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: postgres-data
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 100Gi
  storageClassName: fast-ssd
```

---

## 4. PersistentVolume (PV)

PV is the **actual storage resource**.

Examples:
- AWS EBS
- Azure Disk
- NFS
- Local disk

---

### PV Lifecycle

```
Available → Bound → Released → Failed
```

---

### Access Modes

- ReadWriteOnce (RWO)
- ReadOnlyMany (ROX)
- ReadWriteMany (RWX)
- ReadWriteOncePod (RWOP)

👉 Enforced at node level

---

### Reclaim Policies

#### Retain
- Keeps data after PVC deletion
- Manual cleanup required

#### Delete
- Deletes storage automatically

#### Recycle (Deprecated)

---

### PV Example

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-nfs-example
spec:
  capacity:
    storage: 50Gi
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain
  storageClassName: manual
  nfs:
    server: 192.168.1.100
    path: /exports/data
```

---

## 5. StorageClass

Defines how storage is provisioned.

---

### StorageClass Example

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast-ssd
provisioner: ebs.csi.aws.com
parameters:
  type: gp3
reclaimPolicy: Delete
volumeBindingMode: WaitForFirstConsumer
allowVolumeExpansion: true
```

---

### Key Fields

#### provisioner
- CSI driver used

#### volumeBindingMode

- Immediate → provision immediately
- WaitForFirstConsumer → wait for Pod scheduling ✅

#### allowVolumeExpansion
- Allows resizing

---

## Default StorageClass

- Only one default allowed
- If none → PVC stays Pending

---

## Full Read/Write Flow

### Write Path

```
App → Container → Volume → PVC → PV → Storage → Disk
```

---

### Read Path

```
Disk → Storage → PV → PVC → Volume → Container → App
```

---

## Troubleshooting

### PVC stuck in Pending
- No matching PV
- StorageClass issue

---

### Pod stuck in ContainerCreating
- Volume mount failure
- Storage attach issue

---

## Key Takeaways

- Volume = mount point + connector
- PVC = request
- PV = actual storage
- StorageClass = provisioning logic

---

## Final Insight

Volumes are the entry point to storage inside a Pod, but persistent storage is provided through the combination of PVC, PV, and StorageClass.

👉 Understanding this flow is critical for debugging and exams.
