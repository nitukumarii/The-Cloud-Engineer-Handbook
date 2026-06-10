# Editing a Kubernetes Deployment (YAML vs Command)

---

## 📌 Question

If you already have a **YAML file for a Deployment**, how should you edit and apply changes correctly?

---

## ✅ Recommended Approach (Declarative – Best Practice)

### 🔹 Step 1: Edit YAML File Locally

```bash
vi deployment.yaml
```

👉 You can modify:

* image version
* replicas
* ports
* environment variables

---

### 🔹 Step 2: Apply Changes

```bash
kubectl apply -f deployment.yaml
```

---

### 🔹 What Happens Internally

* Kubernetes compares:

  * Current state (running Deployment)
  * Desired state (YAML file)

* Then it:

  * Updates only required changes
  * Performs rolling updates (if needed)

---

### 🔹 Advantages

✔ Changes are **tracked in file**
✔ Can store in **Git (version control)**
✔ Safe for **production environments**
✔ Follows **declarative approach**

---

## ❌ Alternative Approach (Imperative – Not Recommended)

### 🔹 Edit Live Deployment Directly

```bash
kubectl edit deployment my-app
```

---

### 🔹 What Happens

* Opens live configuration
* You edit and save
* Changes applied immediately

---

### ⚠️ Problems

❌ Changes are **NOT saved in YAML file**
❌ No version control
❌ Can cause mismatch between:

* Local file
* Actual cluster

---

## 📌 When to Use kubectl edit?

✔ Quick fixes
✔ Debugging
✔ Temporary changes

❌ Not for production changes

---

## 🎯 Interview Answer

👉 “If I have a YAML file, I update it locally and apply changes using `kubectl apply -f file.yaml`. I avoid `kubectl edit` in production because it does not persist changes in version-controlled files.”

---

## ⚡ Quick Summary

| Method        | Command                            | Use Case    |
| ------------- | ---------------------------------- | ----------- |
| Declarative ✅ | `kubectl apply -f deployment.yaml` | Production  |
| Imperative ❌  | `kubectl edit deployment my-app`   | Quick fixes |

---
