
## Kubernetes Pod Spec (with memory request & limit)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: demo-app
spec:
  containers:
  - name: app-container
    image: nginx:latest
    resources:
      requests:
        memory: "256Mi"
        cpu: "200m"
      limits:
        memory: "512Mi"
        cpu: "500m"
```
