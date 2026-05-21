## 🔄 Update Strategies

---

### 1️⃣ RollingUpdate (Default)

- Updates pods one-by-one
- Order: highest → lowest

```
web-2 → web-1 → web-0
```

---

### 2️⃣ OnDelete

- Pods NOT updated automatically
- You must delete pods manually

---
