## 🧩 StatefulSet YAML Structure

```yaml
apiVersion: apps/v1
kind: StatefulSet

metadata:
  name: web

spec:
  serviceName: "nginx"   # Headless Service
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

## 🔍 Important Fields Explained

---

### 🔹 serviceName

- Links to Headless Service
- Required for DNS

---

### 🔹 replicas

- Number of Pods

---

### 🔹 selector

- Must match template labels

---

### 🔹 template

- Defines Pod configuration

---

### 🔹 volumeClaimTemplates (VERY IMPORTANT)

- Creates one storage per pod
- Automatically generates PVCs

---
