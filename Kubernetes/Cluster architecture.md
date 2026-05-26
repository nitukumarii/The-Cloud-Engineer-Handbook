# Kubernetes Architecture (Interview-Ready Notes + Questions)

## Core Idea

Kubernetes is a **container orchestration system** that manages:
- Deployment
- Scaling
- Networking
- Self-healing

👉 It works as a **continuous reconciliation system**: 

Kubernetes is a continuous reconciliation system because it constantly compares the desired state defined by the user with the actual state of the cluster and automatically takes actions to make them match.

```
Desired State → Actual State (maintained automatically)
```

---

# 🧠 Control Plane Components (Brain)

## 1. kube-apiserver

### Concept
- Entry point of Kubernetes
- All communication goes through it
- Validates and processes requests
- Stores state in etcd

👉 Simple:
“kube-apiserver is the front door of Kubernetes.”

---

## Why API Server is Critical

- Single source of communication
- Ensures consistency
- Enforces security (authn/authz)
- Maintains cluster integrity

---

## Failure Impact

- If API server is down:
  - ❌ Cannot create/update resources
  - ❌ kubectl stops working
  - ✅ Existing Pods keep running

---

### Interview Questions

**Q1: What is kube-apiserver?**  
→ Entry point that handles all API requests.

**Q2: Can components talk directly to each other?**  
→ ❌ No, all communication goes through API server.

→ Only control plane communication goes through it  
→ Pod-to-Pod traffic does NOT

All management-related communication goes through kube-apiserver:

- kubectl → API server  
- kubelet → API server  
- scheduler → API server  
- controller manager → API server  

👉 Rule:
```
All cluster state changes go through API server
```

---

### ❌ Data Plane Communication (Does NOT go through API Server)

Application traffic does NOT use the API server:

- Pod → Pod communication  
- Pod → Service communication  
- Service → Pod routing  

👉 These use:
- CNI (network plugins)
- kube-proxy

---

## Example Flows

### 1. Creating a Pod

```
kubectl apply → API server → etcd
                        ↓
                   scheduler
                        ↓
                    kubelet
```

---

### 2. Pod-to-Pod Communication

```
Pod A → Pod B (direct network)
```

👉 API server is NOT involved

---

**Q3: What happens when you run `kubectl apply`?**  
→ Request goes to API server → validated → stored in etcd.

---

## 2. etcd

### Concept
- Distributed key-value store
- Stores:
  - cluster state
  - pods
  - nodes
  - configs

👉 Source of truth

---

### Interview Questions

**Q1: What is etcd used for?**  
→ Stores cluster state.

**Q2: Does etcd schedule pods?**  
→ ❌ No

**Q3: What happens if etcd is lost?**  
→ Cluster state is lost → cluster breaks

---

## 3. kube-scheduler

### Concept
- Decides **which node a Pod runs on**
- Based on:
  - CPU/memory
  - node capacity
  - affinity/anti-affinity
  - taints/tolerations

👉 Important:
- Scheduler ONLY decides placement

---

### Interview Questions

**Q1: Does scheduler run containers?**  
→ ❌ No

**Q2: What factors does scheduler consider?**  
→ Resources, constraints, policies

**Q3: What if no node matches?**  
→ Pod stays in Pending

---

## 4. kube-controller-manager

### Concept
- Runs controllers
- Maintains:
```
Desired State = Actual State
```

Examples:
- ReplicaSet controller
- Node controller
- Job controller

👉 Continuously watches cluster

---

### Interview Questions

**Q1: What is a controller?**  
→ A loop that ensures desired state is maintained

**Q2: Does controller schedule pods?**  
→ ❌ No

**Q3: What happens if a Pod crashes?**  
→ Controller recreates it

---

# ⚙️ Worker Node Components (Execution Layer)

## 5. kubelet

### Concept
- Runs on each node
- Talks to API server
- Ensures containers are running

👉 MOST IMPORTANT:
- kubelet actually executes workloads

---

### Interview Questions

**Q1: Who runs containers in Kubernetes?**  
→ kubelet (via container runtime)

**Q2: What happens if kubelet stops?**  
→ Node becomes NotReady

---

## 6. Container Runtime

### Concept
- Runs containers

Examples:
- containerd
- CRI-O

👉 Without this → containers cannot run

---

### Interview Questions

**Q1: Is Docker required in Kubernetes?**  
→ ❌ No

**Q2: What does runtime do?**  
→ Pulls images and runs containers

---

## 7. kube-proxy

### Concept
- Handles networking
- Maintains iptables/IPVS rules
- Enables:
  - Service → Pod communication

---

### Interview Questions

**Q1: What is kube-proxy?**  
→ Networking component

**Q2: How do services reach pods?**  
→ Through kube-proxy rules

---

# 📦 Core Kubernetes Objects

## Pod

### Concept
- Smallest deployable unit
- Contains one or more containers

---

### Interview Questions

**Q1: Can a Pod have multiple containers?**  
→ ✅ Yes

**Q2: Do containers in a Pod share network?**  
→ ✅ Yes

---

## Node

### Concept
- Machine (VM/EC2/server)
- Runs Pods

👉 Important:
- 1 EC2 = 1 Node

---

### Interview Questions

**Q1: What is a Node?**  
→ Machine that runs Pods

**Q2: Is node a group of machines?**  
→ ❌ No

---

# 🔌 Additional Important Components

## CoreDNS

### Concept
- Internal DNS system
- Resolves service names

Example:
```
my-service.default.svc.cluster.local
```

---

### Interview Questions

**Q1: How do Pods find services?**  
→ Using DNS (CoreDNS)

---

## Cloud Controller Manager

### Concept
- Integrates with cloud providers
- Manages:
  - load balancers
  - volumes
  - node lifecycle

---

### Interview Questions

**Q1: What does cloud controller manager do?**  
→ Connects Kubernetes with cloud services

---

# 🔄 Complete Flow (VERY IMPORTANT)

```
1. User → kubectl
2. Request → kube-apiserver
3. State stored → etcd
4. Scheduler picks node
5. kubelet runs Pod
6. Container runtime starts container
7. kube-proxy enables networking
```

---

# 🔁 System Behavior (Deep Insight)

Kubernetes is a **continuous loop system**:

```
Desired State → API Server → Scheduler → kubelet → Actual State
                      ↑                          ↓
                  Controllers ←───────────────────
```

---

# ⚡ Key Insights (Must Remember)

- API Server = entry point
- etcd = source of truth
- Scheduler = decision maker
- kubelet = executor
- Controllers = self-healing
- kube-proxy = networking
- Runtime = runs containers

---

# 🚨 Common Mistakes

❌ etcd schedules pods → WRONG  
❌ controller manager schedules pods → WRONG  
❌ node = group of EC2 → WRONG  

---

# 🎯 One-Line Interview Answer

“Kubernetes control plane consists of API server, scheduler, controller manager, and etcd. API server handles requests, etcd stores state, scheduler assigns pods to nodes, and controller manager ensures desired state. On worker nodes, kubelet runs pods, container runtime executes containers, and kube-proxy handles networking.”

---

# ✅ Final Takeaway

👉 Kubernetes is a **declarative, self-healing system**

You define:
```
Desired State
```

Kubernetes ensures:
```
It is always true
```
