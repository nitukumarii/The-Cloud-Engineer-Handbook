# How to check TargetPort configured on a Kubernetes Service

## 1. Get full service details
kubectl get svc <service-name> -n <namespace>

kubectl describe svc <service-name> -n <namespace>

➡️ In the output look for:
Port:
TargetPort:

Example:
Port:        80/TCP
TargetPort:  8080/TCP


## 2. Get targetPort in JSONPath (clean output)
kubectl get svc <service-name> -n <namespace> -o jsonpath='{.spec.ports[*].port} {.spec.ports[*].targetPort}'

Example output:
80 8080


## 3. Get detailed YAML view
kubectl get svc <service-name> -n <namespace> -o yaml

➡️ Look under:
spec:
  ports:
    - port: 80
      targetPort: 8080


## 4. Check endpoint mapping (to verify actual backend port)
kubectl get endpoints <service-name> -n <namespace>

or

kubectl describe endpoints <service-name> -n <namespace>

➡️ This shows which pod IPs and ports are actually receiving traffic


## 5. If targetPort is named (not number)
kubectl get svc <service-name> -n <namespace> -o yaml

Example:
targetPort: http

➡️ Then check container port in deployment:
kubectl get deploy <deployment-name> -n <namespace> -o yaml

Look for:
containerPort: 8080


## Summary
- spec.ports.port = service port
- spec.ports.targetPort = container/pod port
- Endpoints confirm actual runtime mapping
