# Kubernetes Day 2 — YAML & Pods 🚀

## What I Learned

Today I learned how to create and manage Kubernetes resources using **YAML files**.

### Topics Covered

* Kubernetes YAML
* `apiVersion`
* `kind`
* `metadata`
* `spec`
* Containers
* Container images
* Labels
* Label selectors
* Declarative approach
* `kubectl apply`
* `kubectl delete`

## Hands-on Practice

### Create Pod YAML

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx
  labels:
    app: web

spec:
  containers:
    - name: nginx
      image: nginx
```

### Apply YAML

```bash
kubectl apply -f pod.yaml
```

### Check Pods

```bash
kubectl get pods
```

### Show Labels

```bash
kubectl get pods --show-labels
```

### Get Pods Using Label

```bash
kubectl get pods -l app=web
```

### Delete Resource

```bash
kubectl delete -f pod.yaml
```

## Key Learning

### Imperative

```bash
kubectl run nginx --image=nginx
```

Tell Kubernetes what to do.

### Declarative

```bash
kubectl apply -f pod.yaml
```

Tell Kubernetes the desired state.

