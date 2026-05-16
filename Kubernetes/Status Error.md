# Kubernetes Errors – Direct Causes & How to Explain (Interview Ready)

---

## 1. Pending State


A Pod remains in Pending when it has been accepted by Kubernetes but cannot move to the Running state. This typically happens due to issues in either scheduling or initialization.

**1. Scheduling Phase (most common):**
The Kubernetes scheduler is unable to place the Pod on any node because no node satisfies the constraints defined in the Pod spec. Common reasons include:

Insufficient CPU, memory, or ephemeral storage 

Node selector or affinity mismatch

Taints and tolerations not aligned

Topology constraints not satisfied

Node conditions like NotReady or DiskPressure

In this case, the Pod is Pending because the scheduler is rejecting the Pod specification, not because the cluster is unhealthy.

**2. Post-Scheduling Phase (scheduled but not running):**
Even after a node is assigned, the Pod can remain Pending if the node cannot complete initialization. This can happen due to:

Image pull delays or failures

Init containers still running

Volume mount or PVC binding delays

Missing or delayed secrets/configMaps


How to debug:

The most reliable approach is to run:

kubectl describe pod <pod-name>

and check the Events section, which clearly indicates whether the issue is scheduling-related or initialization-related.

Key insight:
In real production environments, most Pending Pods are caused by scheduling constraints or misconfigurations, not infrastructure failure.

One-line summary:
A Pod stays Pending either because no suitable node is available for scheduling, or because the node cannot successfully initialize the Pod after scheduling.


---

## 2. CrashLoopBackOff

👉 Meaning: Container is **starting → crashing → restarting repeatedly**

### Direct Causes:

* Application crash (bug)
* OOMKilled (memory limit exceeded)
* Wrong command / entrypoint
* Missing config / secret
* Dependency failure (DB/API not reachable)
* Liveness probe failure

### Important Clarification:

* Happens **after container starts**
* So ❌ NOT due to insufficient memory (scheduling issue)
* ✅ Can be due to **OOM (runtime issue)**

### What to say:

“CrashLoopBackOff is not a root cause, it indicates repeated container failures.”

---

## 3. OOMKilled

👉 Meaning: Container exceeded memory limit

### Direct Causes:

* Memory limit too low
* Application memory leak
* Sudden spike in usage

### What to say:

“OOMKilled happens at runtime when container exceeds its memory limit, not during scheduling.”

---

## 4. ImagePullBackOff

👉 Meaning: Kubernetes is retrying to pull image with backoff

### Direct Causes:

* Wrong image name/tag
* Private repo authentication failure
* Network issue
* Registry not reachable

### What to say:

“ImagePullBackOff means Kubernetes failed to pull image and is retrying with delay.”

---

## 5. ErrImagePull

👉 Meaning: Immediate failure while pulling image

### Direct Causes:

* Invalid image name
* Image does not exist
* Authentication failure

### Difference from ImagePullBackOff:

* ErrImagePull → first failure
* ImagePullBackOff → retry with delay

---

## 6. CreateContainerConfigError

👉 Meaning: Configuration issue before container starts

### Direct Causes:

* Missing ConfigMap
* Missing Secret
* Wrong environment variables

### What to say:

“Configuration error preventing container from starting.”

---

## 7. CreateContainerError

👉 Meaning: Container creation failed

### Direct Causes:

* Invalid command
* Missing binary/file
* Permission issues

---

## 8. ContainerCannotRun

👉 Meaning: Container cannot execute

### Direct Causes:

* Wrong entrypoint
* Invalid command
* Permission denied

---

## 9. RunContainerError

👉 Meaning: Container started but failed immediately

### Direct Causes:

* Runtime failure
* Dependency crash

---

## 10. Evicted

👉 Meaning: Pod removed from node

### Direct Causes:

* Node memory pressure
* Disk pressure

### What to say:

“Evicted happens when node is under resource pressure, not due to container limits.”

---

## 11. Probe Failures

### Liveness Probe Failure

* Causes container restart

### Direct Causes:

* App not responding
* Wrong probe config

---

### Readiness Probe Failure

* Pod not added to service

### Direct Causes:

* App not ready
* Dependency not available

---

## 12. Node Issues

### NodeNotReady

### Direct Causes:

* Node down
* Network issue
* kubelet failure

---

## 13. Quick Interview Summary

Most important errors:

* Pending → scheduling issue
* CrashLoopBackOff → repeated crash
* OOMKilled → memory limit exceeded
* ImagePullBackOff → image issue
* ErrImagePull → initial image failure
* CreateContainerConfigError → config issue
* Evicted → node pressure

---

## 14. Key Interview Clarifications (VERY IMPORTANT)

* CrashLoopBackOff happens **after container starts**
* Insufficient memory → **Pending**, not CrashLoopBackOff
* OOM → runtime → can cause CrashLoopBackOff
* Image errors → container never starts

---

## 15. Strong One-Liner

“Kubernetes errors can be categorized into scheduling issues like Pending, runtime failures like OOMKilled, restart loops like CrashLoopBackOff, image issues like ImagePullBackOff, and node-level issues like Evicted.”
