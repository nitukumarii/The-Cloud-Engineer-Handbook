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

