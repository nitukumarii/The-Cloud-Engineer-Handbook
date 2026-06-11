# Creating a Deployment YAML Using kubectl (Imperative → Declarative)

## Problem

Command executed:

```bash id="e6ysfe"
kubectl create deployment webapp -image:kodekloud/webapp-color --replicas=3 --dry-run=client -o yaml > webapp.yaml
```

Error:

```text id="f8v7ha"
error: unknown shorthand flag: 'i' in -image:kodekloud/webapp-color
```

---

## Cause

### Incorrect Syntax

```bash id="s86jpl"
-image:kodekloud/webapp-color
```

Issues:

* `-image` should be `--image`
* `:` should be `=`

---

## Correct Command

```bash id="y3l9jv"
kubectl create deployment webapp --image=kodekloud/webapp-color --replicas=3 --dry-run=client -o yaml > webapp.yaml
```

This command:

* Creates a Deployment named `webapp`
* Uses image `kodekloud/webapp-color`
* Creates `3` replicas
* Does not create the resource in the cluster (`--dry-run=client`)
* Outputs the manifest as YAML (`-o yaml`)
* Saves the YAML to `webapp.yaml`

---

## View the Generated YAML

```bash id="4l8p87"
cat webapp.yaml
```

or

```bash id="m6z1r4"
vi webapp.yaml
```

---

## Create the Deployment

```bash id="svykk4"
kubectl create -f webapp.yaml
```

---

## Verify

```bash id="6qngm0"
kubectl get deployments
```

```bash id="h2gtvg"
kubectl get pods
```

---

## Generated YAML (Example)

```yaml id="od8l8g"
apiVersion: apps/v1
kind: Deployment
metadata:
  name: webapp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: webapp
  template:
    metadata:
      labels:
        app: webapp
    spec:
      containers:
      - name: webapp-color
        image: kodekloud/webapp-color
```

---

## CKA/CKAD Exam Shortcut

Generate Deployment YAML:

```bash id="vxq5rj"
kubectl create deployment <name> \
--image=<image> \
--replicas=<count> \
--dry-run=client -o yaml > <file>.yaml
```

Example:

```bash id="a7ecmv"
kubectl create deployment nginx \
--image=nginx \
--replicas=2 \
--dry-run=client -o yaml > nginx.yaml
```

### Remember

```text id="1z1wb4"
YAML      → uses :
kubectl   → uses --flag=value
```

Examples:

```yaml id="t7mkg0"
image: nginx
```

```bash id="b8h7an"
--image=nginx
```
