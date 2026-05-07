Basic initial checks for a pod OOM issue:

1. Check pod events/status:

```bash id="2d03m9"
kubectl describe pod <pod-name> -n <namespace>
```

Look for:

```text id="lybjlwm"
Last State:     Terminated
Reason:         OOMKilled
Exit Code:      137
```

This confirms the container exceeded its memory limit and Kubernetes restarted it.

2. Check previous container logs:

```bash id="c29vkr"
kubectl logs <pod-name> -n <namespace> --previous
```

`--previous` is important because it shows logs from the crashed container instance before restart. This usually contains:

* OutOfMemory errors
* Heap exhaustion
* Memory spike indicators
* Last application activity before termination

3. Check current container logs:

```bash id="h8hzr7"
kubectl logs <pod-name> -n <namespace>
```

Current logs belong to the newly restarted container and usually show:

* Application startup logs
* Initialization messages
* Recovery behavior
* Whether the pod is restarting repeatedly

4. Check restart count:

```bash id="4uxw1r"
kubectl get pod <pod-name> -n <namespace>
```

Frequent restarts may indicate continuous OOM events.

5. Check current memory usage:

```bash id="cvbzfk"
kubectl top pod <pod-name> -n <namespace>
```

This helps compare actual memory usage against configured limits.

6. Verify memory requests and limits:

```bash id="9k0h7x"
kubectl get pod <pod-name> -n <namespace> -o yaml | grep -A5 resources:
```

Example:

```yaml id="sjr4n2"
resources:
  requests:
    memory: "512Mi"
  limits:
    memory: "1Gi"
```

If the application usage exceeds the memory limit, Kubernetes kills the container with `OOMKilled`.

Typical troubleshooting flow:

* describe pod
* previous logs
* current logs
* restart count
* memory usage
* memory limits



**************************************************************************************************
*************************************************************************************************


### Kubernetes OOM, CrashLoopBackOff & Memory Management – Interview Notes

---

## 1. Scheduling vs Runtime (Foundation Concept)

Kubernetes has two separate phases:

### Scheduling Phase

* Based on **resource requests**
* Scheduler checks if node has enough **requested memory**
* If yes → pod is scheduled
* If no → pod stays **Pending**

Example:

```
Status: Pending
Reason: Insufficient memory
```

👉 Key point:

* Pod is **never created**
* Container **never starts**
* **OOM cannot happen here**

---

### Runtime Phase

* Happens after pod is scheduled and container starts
* Memory usage is enforced using **limits**
* If container exceeds limit → **OOMKilled**

---

## 2. Requests vs Limits (Very Important)

### Requests

* Minimum memory required
* Used only for **scheduling**
* Guarantees placement on node

### Limits

* Maximum memory allowed
* Enforced at runtime
* If exceeded → container is **killed**

👉 Rule to remember:

* High requests → pod not scheduled
* Low limits → pod runs but gets OOMKilled

---

## 3. What is OOMKilled?

OOM (Out Of Memory) occurs when:

* Container uses more memory than its **limit**

Kubernetes behavior:

* Kills container immediately
* Exit code: `137`

Example:

```
Reason: OOMKilled
Exit Code: 137
```

👉 Important:

* Pod **was scheduled successfully**
* Container **was running**
* Then exceeded limit → killed

---

## 4. OOM Flow (Step-by-Step)

1. Pod scheduled (based on requests)
2. Container starts
3. Application consumes memory
4. Memory exceeds limit
5. Container killed → OOMKilled
6. Restart happens
7. If repeated → CrashLoopBackOff

---

## 5. CrashLoopBackOff Explained

CrashLoopBackOff means:

* Container keeps restarting repeatedly due to failure

Flow:

```
Start → Crash → Restart → Crash → Restart → Backoff delay
```

👉 Direct causes:

* Application crash
* OOMKilled
* Wrong command/entrypoint
* Liveness probe failure
* Config/dependency failure during startup

---

## 6. OOM vs CrashLoopBackOff Relationship

* OOMKilled is a **cause**
* CrashLoopBackOff is a **result of repeated failures**

Example:

```
Reason: OOMKilled
Status: CrashLoopBackOff
```

---

## 7. Logs Understanding (Very Important in Interviews)

After restart:

### Current Logs

```
kubectl logs <pod>
```

* Logs of **new container**
* Shows startup and current behavior

---

### Previous Logs

```
kubectl logs <pod> --previous
```

* Logs of **crashed container**
* Most important for OOM debugging

👉 Always check `--previous` first in OOM cases

---

## 8. Basic Troubleshooting Flow

1. Check events/status:

```
kubectl describe pod <pod>
```

2. Check previous logs:

```
kubectl logs <pod> --previous
```

3. Check current logs:

```
kubectl logs <pod>
```

4. Check restart count:

```
kubectl get pod <pod>
```

5. Check memory usage:

```
kubectl top pod <pod>
```

6. Check memory config:

```
kubectl get pod <pod> -o yaml
```

---

## 9. Node-Level OOM vs Container OOM

### Container OOM

* Exceeds **its own limit**
* Result → `OOMKilled`

---

### Node-Level OOM (Eviction)

* Node runs out of memory
* Kubernetes evicts pods

Example:

```
Status: Evicted
Reason: MemoryPressure
```

👉 Difference:

* OOMKilled → container issue
* Evicted → node issue

---

## 10. QoS Classes (Very Important)

Determines which pods are killed first under memory pressure.

### Guaranteed

* requests = limits
* Highest priority
* Least likely to be killed

---

### Burstable

* requests < limits
* Medium priority

---

### BestEffort

* No requests or limits
* Lowest priority
* Killed first

---

## 11. Why OOM Happens (Practical Reasons)

* Memory limit too low
* Application memory leak
* Sudden traffic spike
* Improper heap/GC configuration (Java, Node, etc.)
* Large data processing in memory

---

## 12. How to Fix OOM

* Increase memory limits
* Optimize application memory usage
* Fix memory leaks
* Tune heap/GC
* Set correct requests/limits
* Use horizontal scaling

---

## 13. Common Interview Traps

❌ “OOM means pod was not scheduled” → WRONG
✅ OOM happens only after pod is running

❌ “Limits affect scheduling” → WRONG
✅ Only requests affect scheduling

❌ “Check current logs first” → Not always
✅ For OOM, check `--previous` logs first

---

## 14. Final Summary (Must Remember)

* Scheduling → based on requests
* Runtime → controlled by limits
* OOM → happens after container starts
* OOMKilled → container exceeded limit
* Repeated failures → CrashLoopBackOff
* `--previous` logs → key for debugging

👉 Core idea:
**Scheduling problem ≠ Runtime memory problem**



\
