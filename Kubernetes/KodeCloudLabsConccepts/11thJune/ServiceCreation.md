# Create a ClusterIP Service named redis-service exposing port 6379

## Imperative Way (Fastest)

If the Redis pod already exists:

```bash
kubectl expose pod redis --name=redis-service --port=6379
```

Or expose a deployment:

```bash
kubectl expose deployment redis --name=redis-service --port=6379
```

Verify:

```bash
kubectl get svc
kubectl describe svc redis-service
```

---

## Generate YAML Imperatively

```bash
kubectl expose pod redis --name=redis-service --port=6379 --dry-run=client -o yaml > redis-service.yaml
```

---

## Declarative YAML

```yaml
apiVersion: v1
kind: Service
metadata:
  name: redis-service
spec:
  type: ClusterIP
  selector:
    tier: db
  ports:
  - port: 6379
    targetPort: 6379
```

Create the service:

```bash
kubectl create -f redis-service.yaml
```

Verify:

```bash
kubectl get svc redis-service
kubectl describe svc redis-service
```
