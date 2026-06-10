# Kubernetes Service Exposure – Question & Answer (Deep Understanding)

---

## ❓ Question

You have a **Deployment running multiple Pods** in Kubernetes.

1. How do you expose this Deployment using a Service?
2. What happens internally when you run the expose command?
3. If the application was initially exposed on port 80 and now needs to be accessed on port 8080, how does it work?
4. Explain both scenarios:

   * Only changing Service port
   * Changing application (container) port

---

## ✅ Answer

---

## 🔹 Step 1: Create Deployment

```bash
kubectl create deployment my-app --image=nginx
```

### 👉 What happens:

* Deployment is created
* Multiple Pods are created
* Each Pod runs container (nginx) on **port 80**

---

## 🔹 Step 2: Expose Deployment

```bash
kubectl expose deployment my-app --port=80 --target-port=80 --type=NodePort
```

---

## 🔹 What This Command Does Internally

In Kubernetes:

### 1. Service Object is Created

* A **Service** is created automatically

```yaml
selector:
  app: my-app
```

---

### 2. Service Connects to Pods via Labels

* Deployment Pods have labels:

```yaml
app: my-app
```

* Service uses selector to find matching Pods

👉 This links:

```
Service → Pods
```

---

### 3. Stable Endpoint is Created

* Pods are dynamic (IP changes)
* Service provides:

  * Stable IP
  * DNS name

👉 Instead of Pod IP, we use:

```
my-app
```

---

### 4. Load Balancing Happens

* Service distributes traffic across all Pods
* Done using kube-proxy (iptables/IPVS)

---

### 5. External Exposure (NodePort Example)

```
User → NodeIP:NodePort → Service → Pod
```

---

## 🔹 Understanding Ports (VERY IMPORTANT)

| Port Type  | Meaning              |
| ---------- | -------------------- |
| port       | Service port         |
| targetPort | Pod/container port   |
| nodePort   | External access port |

---

# 🔥 Scenario 1: Only Service Port Changes

## ❓ Requirement:

App runs on port 80, but user should access on 8080

---

## ✅ Command:

```bash
kubectl expose deployment my-app --port=8080 --target-port=80 --type=NodePort
```

---

## 🔹 What Happens:

* Service listens on **port 8080**
* Pods still run on **port 80**

---

## 🔹 Traffic Flow:

```
User → Service:8080 → Pod:80
```

---

## 🔹 Key Statement:

👉 “Only entry point changes, application remains same”

---

# 🔥 Scenario 2: Application Port Changes (Container)

## ❓ Requirement:

Application now runs on port 8080

---

## ✅ Update Deployment YAML:

```yaml
containers:
  - name: nginx
    image: nginx
    ports:
      - containerPort: 8080
```

---

## ✅ Expose Service:

```bash
kubectl expose deployment my-app --port=80 --target-port=8080 --type=NodePort
```

---

## 🔹 What Happens:

* Service listens on **port 80**
* Pods now run on **port 8080**

---

## 🔹 Traffic Flow:

```
User → Service:80 → Pod:8080
```

---

## 🔹 Key Statement:

👉 “Application port changes, Service forwards traffic accordingly”

---

# 🔥 LoadBalancer vs NodePort vs ClusterIP

## 🔹 LoadBalancer

```
User → LoadBalancer → NodePort → Service → Pod
```

✔ Used in cloud (AWS, Azure)

---

## 🔹 NodePort

```
User → NodeIP:NodePort → Service → Pod
```

---

## 🔹 ClusterIP

```
Internal only:
Service → Pod
```

---

# 🔥 Internal Working Summary

When you run:

```bash
kubectl expose deployment my-app
```

Kubernetes:

1. Creates Service object
2. Reads Deployment labels
3. Matches Pods using selector
4. Configures routing via kube-proxy
5. Enables load balancing
6. Provides stable DNS

---

# 🔥 Real-World Analogy (Interview Gold)

* Deployment = Restaurant
* Pods = Chefs
* Service = Waiter
* LoadBalancer = Main Gate

### Flow:

```
Customer → Gate → Waiter → Chef
```

---

# 🎯 Final Interview Answer

👉 “Exposing a Deployment creates a Service that selects Pods using labels, provides a stable endpoint, and routes traffic from a defined port to the container port. Depending on configuration, the Service can expose the application internally or externally, while Kubernetes handles load balancing and routing automatically.”

---

# ⚡ Key Takeaways

* Service = abstraction over Pods
* Uses labels to connect
* Provides stable access
* Handles load balancing
* Port vs targetPort difference is critical

---
