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

CrashLoopBackOff occurs when a container repeatedly starts, crashes, and Kubernetes restarts it with an increasing backoff delay. The most common causes are:

Configuration issues such as missing environment variables, incorrect ConfigMaps/Secrets, or wrong startup commands
Probe misconfiguration where liveness/readiness probes are too aggressive or incorrectly defined
Resource constraints like low memory limits leading to OOMKilled errors
Application-level failures such as unhandled exceptions or startup issues
External dependency failures like database or API connectivity problems

To troubleshoot CrashLoopBackOff, I follow a structured approach:

1. Identify the failing pod

Run:

kubectl get pods
kubectl describe pod <pod-name>
Check:
Restart Count
Container State (Error / OOMKilled)
Events section

Example output:

NAME                        READY   STATUS             RESTARTS   AGE
demo-app-abc123             0/1     CrashLoopBackOff   5          2m
Events:
  Warning  BackOff    kubelet  Back-off restarting failed container
  Warning  Failed     kubelet  Error: configmap "app-config" not found

👉 Insight: Missing ConfigMap → configuration issue

2. Check logs (most critical step)

Run:

kubectl logs <pod-name> --previous

Example output:

ERROR: missing DB_HOST environment variable
Application failed to start

👉 Insight: Missing environment variable → root cause

3. Validate configuration

Verify:
ConfigMaps and Secrets
Environment variables
Startup commands

👉 In real scenarios, many issues are caused by misconfigured endpoints or missing values

4. Check probes

Look in:

kubectl describe pod

Example output:

Liveness probe failed: HTTP probe failed with statuscode: 404

👉 Insight: Probe misconfiguration → container restarting unnecessarily

5. Check resource limits

Look for:
Last State: Terminated
Reason: OOMKilled
Exit Code: 137

Run:

kubectl top pod

👉 Insight: Memory limit too low → container killed

6. Fix and redeploy

Apply fix:
Configuration correction
Resource tuning
Code or dependency fix

Monitor:

kubectl get pods -w

From an SRE perspective, I also focus on prevention by standardizing probe configurations, setting proper resource limits, improving observability, and converting recurring issues into runbooks and platform improvements.

In my experience, CrashLoopBackOff is usually a symptom of deeper issues, so I focus not only on fixing it quickly but ensuring it doesn’t happen again.

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
