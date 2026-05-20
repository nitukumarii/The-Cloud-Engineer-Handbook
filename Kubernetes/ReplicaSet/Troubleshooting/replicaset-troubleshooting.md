# 🔥 Kubernetes ReplicaSet – Troubleshooting Questions

## 📌 ReplicaSet Behavior
- Why is ReplicaSet not creating Pods?
- Why is ReplicaSet not maintaining desired replica count?
- Why are fewer Pods running than expected?
- Why are too many Pods running?

---

## 📌 Pod Management Issues
- Why are Pods getting deleted automatically by ReplicaSet?
- Why did ReplicaSet recreate a deleted Pod?
- What happens when a Pod fails under a ReplicaSet?
- Does ReplicaSet recreate Pods on the same node or different node?

---

## 📌 Selector & Label Issues (VERY IMPORTANT)
- What happens if selector does not match template labels?
- Why is ReplicaSet not managing any Pods?
- Why is ReplicaSet managing wrong Pods?
- What happens if two ReplicaSets have the same selector?
- Can ReplicaSet adopt existing Pods? When and why?

---

## 📌 Scheduling & Pending Issues
- Why did ReplicaSet create Pod but it is still Pending?
- Why are ReplicaSet Pods not getting scheduled?
- What happens when cluster has insufficient resources?
- How do taints/tolerations affect ReplicaSet Pods?

---

## 📌 Node Failure Scenarios
- What happens when a node crashes?
- Will ReplicaSet recreate Pods on another node?
- Why are Pods missing after node failure?

---

## 📌 Resource Issues
- Why are ReplicaSet Pods unschedulable?
- What happens when CPU/Memory requests are too high?
- How does resource pressure affect ReplicaSet?

---

## 📌 Events & Debugging
- How to debug ReplicaSet issues using `kubectl describe rs`?
- What events should you check in ReplicaSet troubleshooting?
- Why are events more useful than logs in some cases?

---

## 📌 Deletion & Lifecycle Issues
- What happens when ReplicaSet is deleted?
- How to delete ReplicaSet without deleting Pods?
- Why are Pods terminating after ReplicaSet creation?

---

## 📌 Scaling Issues
- Why scaling ReplicaSet is not working?
- How does ReplicaSet decide which Pods to delete during scale down?

---

## 📌 Conceptual / Interview Questions
- What is the responsibility of ReplicaSet vs Scheduler?
- Why is ReplicaSet not responsible for node placement?
- What are limitations of ReplicaSet?
- Why is Deployment preferred over ReplicaSet?

---

## 🎯 Most Asked Interview Questions
- How do you troubleshoot a ReplicaSet not creating Pods?
- What steps do you follow if Pods are not matching selector?
- How do you debug ReplicaSet vs scheduling issue?
- What happens internally when ReplicaSet creates a Pod?
- How do you identify label mismatch issues quickly?
