# Create Redis Pod with Label `tier=db`

## Imperative Way

Create the pod directly:

```bash
kubectl run redis --image=redis:alpine --labels=tier=db
```

Verify:

```bash
kubectl get pods --show-labels
```

---

## Declarative Way

Generate the manifest:

```bash
kubectl run redis --image=redis:alpine --labels=tier=db --dry-run=client -o yaml > redis-pod.yaml
```

Review/Edit the manifest:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: redis
  labels:
    tier: db
spec:
  containers:
  - name: redis
    image: redis:alpine
```

Create the pod from the manifest:

```bash
kubectl create -f redis-pod.yaml
```

Verify:

```bash
kubectl get pods --show-labels
```

Expected Label:

```text
tier=db
```
