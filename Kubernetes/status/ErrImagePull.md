## ErrImagePull / ImagePullBackOff (Kubernetes)

### Meaning
Kubernetes cannot pull the container image from the registry.

- ErrImagePull → Initial failure to pull image  
- ImagePullBackOff → Retries with exponential backoff (10s → 20s → 40s…)

---

### 1. Root Causes

**Image Issues**
- Incorrect image name / tag / digest  
- Image does not exist (manifest not found)  
- Missing latest tag  

**Authentication Issues**
- Private registry without valid credentials  
- Missing or incorrect imagePullSecrets  

**Network / DNS Issues**
- Node cannot reach registry  
- DNS resolution failure  
- Firewall / proxy blocking access  

**Rate Limiting**
- Too many requests (429 errors)

**Architecture Mismatch**
- Image not compatible with node (ARM vs AMD)

---

### 2. Debug Steps

**Check Pod Events**
```bash
kubectl describe pod <pod-name> -n <namespace>
