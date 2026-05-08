# Kubernetes Errors – Direct Causes & How to Explain (Interview Ready)

---

## 1. Pending State

👉 Meaning: Pod is **not scheduled or not started**

### Direct Causes:

* Insufficient CPU
* Insufficient Memory
* No nodes available
* Node selector / affinity mismatch
* Taints & tolerations mismatch

### What to say:

“Pending means the pod is not scheduled. Most common reason is insufficient resources on nodes.”

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
