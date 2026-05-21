## ⚡ Advanced Concept: Partition Update

```yaml
partition: 1
```

👉 Meaning:
- Only update pods with index ≥ 1
- Used for controlled updates

---

## 📦 Storage Behavior (VERY IMPORTANT)

👉 Volumes are NOT deleted automatically

Even if:
- Pod deleted ❌
- StatefulSet deleted ❌

👉 You must delete PVC manually

---
