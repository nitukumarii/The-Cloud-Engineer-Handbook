# Updating Image in Kubernetes Deployment (Best Practice)

---

## 📌 Question

What is the best way to update the container image in a Kubernetes Deployment?

Should we use:

* `kubectl set image`
* `kubectl edit (vi)`
* OR update YAML file?

---

## ✅ Best Practice (Declarative Approach)

### 🔹 Step 1: Edit YAML File

```bash
vi deployment.yaml
```

Update image:

```yaml
containers:
  - name: nginx
    image: nginx:1.25
```

---

### 🔹 Step 2: Apply Changes

```bash
kubectl apply -f deployment.yaml
```

---

### 🔹 Why This is Best

✔ Changes are stored in YAML
✔ Can be version controlled (Git)
✔ Safe for production
✔ Follows declarative model
✔ Easy to rollback and track

---

## ⚡ Alternative 1: kubectl set image (Quick Method)

```bash
kubectl set image deployment/my-app nginx=nginx:1.25
```

---

### ✔ Pros

* Fast and simple
* Useful in exams
* Triggers rolling update

---

### ❌ Cons

* Not saved in YAML
* Not tracked in Git
* Breaks GitOps workflow

---

## ❌ Alternative 2: kubectl edit (vi)

```bash
kubectl edit deployment my-app
```

---

### ❌ Problems

* Changes not saved in YAML file
* No version control
* Risky in production
* Hard to audit changes

---

## 📌 When to Use What

| Method        | Command                            | Use Case         |
| ------------- | ---------------------------------- | ---------------- |
| Declarative ✅ | `kubectl apply -f deployment.yaml` | Production       |
| Imperative ⚡  | `kubectl set image`                | Quick fix / exam |
| Manual ❌      | `kubectl edit`                     | Debug only       |

---

## 🎯 Interview Answer

👉 “The best practice is to update the image in the YAML file and apply it using `kubectl apply`. `kubectl set image` is useful for quick updates, while `kubectl edit` should be avoided in production as it is not tracked.”

---

## ⚡ Final Summary

* Best → YAML + apply ✅
* Fast → set image ⚡
* Avoid → edit ❌

---
