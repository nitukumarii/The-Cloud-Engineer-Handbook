# 🧠 Step-by-Step: Creating a Pod

## 1️⃣ kubectl apply

```bash
kubectl apply -f pod.yaml
```

👉 You (the user) send a request to create a Pod.

---

## 2️⃣ API Server (Entry Point)

```
kubectl → API server
```

👉 The request first goes to kube-apiserver

### What API server does:
- Authenticates you
- Authorizes the request (RBAC)
- Validates YAML
- Accepts the request

✔ If valid → moves forward  
❌ If invalid → rejects  

---

## 3️⃣ etcd (Store Desired State)

```
API server → etcd
```

👉 The Pod definition is stored in etcd

### Important:
- This is now the **Desired State**
- Pod is NOT running yet

---

## 4️⃣ Scheduler (Decides WHERE)

```
etcd → scheduler
```

👉 Scheduler sees:
> “There is a Pod without a node”

### It decides:
- Which node should run the Pod  
- Based on:
  - CPU/memory  
  - constraints  
  - policies  

✔ Then updates API server:

```
Pod → assigned to Node X
```

---

## 5️⃣ kubelet (Executes)

```
scheduler → kubelet (via API server)
```

👉 kubelet on the selected node:

- Watches API server  
- Sees: “Pod assigned to me”  

### kubelet actions:
- Pulls container image  
- Starts container using runtime  

---

## 6️⃣ Pod is Running

```
kubelet → container runtime → Pod running
```

👉 Now the Pod is actually running on the node  

---

# 🔄 Full Flow (Clean View)

```
1. kubectl apply
2. API server (validate + accept)
3. etcd (store desired state)
4. scheduler (choose node)
5. kubelet (execute)
6. container runtime (run container)
```

---

# ⚡ Key Insights

🔥 API server is always involved  
- Every step goes through it  
- No direct communication  

🔥 Scheduler does NOT run Pods  
- Only assigns node  

🔥 kubelet actually runs Pods  
- Real execution happens here  

🔥 etcd only stores state  
- Does not execute anything  

---

# 🎯 One-Line Interview Answer

> When a Pod is created, the request goes to the API server, which stores it in etcd. The scheduler assigns the Pod to a node, and the kubelet on that node pulls the image and starts the container.
