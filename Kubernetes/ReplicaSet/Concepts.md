# 🚀 Kubernetes ReplicaSet - Concepts

---

## 🔹 Core Components

### 1. Replicas
- Number of Pods to maintain
- Default = 1

---

### 2. Selector (VERY IMPORTANT)
- Identifies Pods using labels
- Must match template labels

---

### 3. Pod Template
- Blueprint for creating Pods

---

## 🔹 How ReplicaSet Works

- Watches Pods using label selectors  
- Creates/deletes Pods to match desired state  
- Tracks Pods using ownerReferences  

---

## 🔹 OwnerReferences

- Links Pod to ReplicaSet
- Helps manage lifecycle

---

## 🔹 Pod Acquisition

ReplicaSet can adopt existing Pods if:
- Labels match selector
- Pod has no owner

⚠️ May delete extra Pods if replicas exceeded

---

## 🔹 Self-Healing

- Failed Pod → automatically recreated

---

## 🔹 Scaling

```bash
kubectl scale rs <name> --replicas=5
```

---

## 🔹 Scheduler vs ReplicaSet

- ReplicaSet → ensures Pod count  
- Scheduler → decides node placement  
- Kubelet → runs container  

---

## 🔹 Node Failure Scenario

If a node crashes:
- Pods on that node are lost  
- ReplicaSet creates new Pods  
- Scheduler places Pods on healthy nodes  

---

## 🔹 Pod Scheduling Question (IMPORTANT)

If a pod fails on Node1:

ReplicaSet creates a new Pod, but does NOT decide node placement.

Scheduler decides:
- Same node (if healthy)
- Different node (if needed)

---

## 🔹 Selector Rules (CRITICAL)

- Selector must match template labels  
- Otherwise → ReplicaSet creation fails  

---

## 🔹 Selector Overlap Issue

If two ReplicaSets have same selector:
- Conflict occurs  
- Pods may be incorrectly managed  

---

## 🔹 Pod Deletion Strategy

When scaling down:
- Pending Pods removed first  
- Lower deletion cost removed first  
- Newer Pods removed first  

---

## 🔹 Limitations

- No rolling updates  
- No rollback  
- No versioning  

---

## 🔹 Real-world Usage

ReplicaSet is rarely used directly.

👉 Deployment is preferred.

---

## 🎯 Summary

ReplicaSet handles desired state and self-healing, while scheduler handles placement decisions.
