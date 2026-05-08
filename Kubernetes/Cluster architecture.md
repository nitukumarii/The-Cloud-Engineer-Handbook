# Kubernetes Components – Correct & Interview-Ready Explanation

## Control Plane Components (Brain of Kubernetes)

### 1. kube-apiserver

* Entry point of Kubernetes
* All requests (kubectl, UI, API) go through this
* Validates and processes requests
* Communicates with etcd

👉 Simple line:
“kube-apiserver is the front door of Kubernetes.”

---

### 2. etcd

* Key-value database
* Stores **cluster state** (pods, nodes, configs, secrets)
* Source of truth

👉 Correction:

* It does NOT schedule pods
* It only stores data

---

### 3. kube-scheduler

* Decides **which node** a pod should run on
* Based on:

  * resource requests
  * node capacity
  * constraints (taints, affinity, etc.)

👉 Your line (corrected):
“Scheduler places pods on nodes based on requested resources.”

---

### 4. kube-controller-manager

* Runs multiple controllers
* Ensures **desired state = actual state**

Examples:

* ReplicaSet controller → ensures correct number of pods
* Node controller → monitors node health
* Job controller → manages jobs

👉 Correction:

* It does NOT send request to etcd to schedule pods
* It watches API server and tries to fix differences

---

## Worker Node Components (Where Pods Run)

### 5. kubelet

* Runs on each node
* Talks to API server
* Ensures containers are running as expected
* Starts/stops containers

👉 Very important (you missed this)

---

### 6. container runtime

* Actually runs containers

Examples:

* containerd
* CRI-O

👉 Without this → containers cannot run

---

### 7. kube-proxy

* Handles networking for pods
* Maintains iptables/ipvs rules
* Enables **service → pod communication**

👉 Simple:
“kube-proxy handles networking and load balancing inside cluster.”

---

## Core Kubernetes Objects

### Pod

* Smallest deployable unit
* Contains one or more containers

---

### Node

* A machine (VM/EC2/server)
* Runs pods

👉 Correction:

* Not a group of EC2 instances
* Each EC2 = one node

---

## Components You Missed (Important)

### 8. CoreDNS

* Internal DNS of Kubernetes
* Resolves service names to IPs

Example:

```text
my-service.default.svc.cluster.local
```

---

### 9. Cloud Controller Manager (if using cloud)

* Integrates with cloud providers (AWS, Azure, GCP)
* Manages:

  * load balancers
  * volumes
  * node lifecycle

---

## Correct Flow (VERY IMPORTANT for interview)

1. User sends request → kube-apiserver
2. API server stores state in etcd
3. Scheduler picks node for pod
4. kubelet on that node starts container
5. kube-proxy enables networking

---

## Quick Summary (What you should say)

* API server → entry point
* etcd → stores state
* Scheduler → assigns pods to nodes
* Controller manager → maintains desired state
* kubelet → runs pods on node
* kube-proxy → networking
* container runtime → runs containers

---

## Common Mistakes (you made these)

❌ etcd schedules pods → WRONG
❌ controller manager schedules pods → WRONG
❌ node = group of EC2 → WRONG

---

## One-line Interview Answer

“Kubernetes control plane consists of API server, scheduler, controller manager, and etcd. API server handles requests, etcd stores state, scheduler assigns pods to nodes, and controller manager ensures desired state. On worker nodes, kubelet runs pods, container runtime executes containers, and kube-proxy handles networking.”
