# Kubernetes Namespace Commands

## View Namespaces

# List all namespaces
kubectl get namespaces

# Short form
kubectl get ns

# Describe a namespace
kubectl describe namespace dev

---

## Working with Resources in Namespaces

# List pods in default namespace
kubectl get pods

# List pods in kube-system namespace
kubectl get pods -n kube-system

# Alternative syntax
kubectl get pods --namespace=kube-system

# List pods in all namespaces
kubectl get pods --all-namespaces

# Short form
kubectl get pods -A

# Get all resources in a namespace
kubectl get all -n dev

---

## Creating Namespaces

# Create namespace using command
kubectl create namespace dev

# Create namespace using YAML
kubectl apply -f namespace.yaml

Example:

apiVersion: v1
kind: Namespace
metadata:
  name: dev

---

## Creating Resources in a Namespace

# Create resource in specific namespace
kubectl apply -f pod.yaml -n dev

# Create resource defined with namespace in YAML
metadata:
  name: nginx
  namespace: dev

---

## Switching Default Namespace

# Set current context namespace to dev
kubectl config set-context --current --namespace=dev

# Switch to prod
kubectl config set-context --current --namespace=prod

After setting default namespace:

kubectl get pods

Will automatically show pods from that namespace.

---

## Check Current Namespace

# Display current namespace
kubectl config view --minify --output 'jsonpath={..namespace}'

---

## Delete Namespace

# Delete namespace
kubectl delete namespace dev

# Short form
kubectl delete ns dev

---

## Resource Quotas

# Create resource quota
kubectl apply -f quota.yaml

Example:

apiVersion: v1
kind: ResourceQuota
metadata:
  name: compute-quota
  namespace: dev
spec:
  hard:
    pods: "10"
    requests.cpu: "2"
    requests.memory: 5Gi
    limits.cpu: "4"
    limits.memory: 10Gi

---

## Useful Interview Commands

# List namespaces
kubectl get ns

# List all pods across namespaces
kubectl get pods -A

# List resources in a namespace
kubectl get all -n dev

# Switch namespace permanently
kubectl config set-context --current --namespace=dev

# Create namespace
kubectl create namespace dev

# Delete namespace
kubectl delete namespace dev

# Check current namespace
kubectl config view --minify --output 'jsonpath={..namespace}'
