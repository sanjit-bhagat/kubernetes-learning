# Kubernetes Day 3 — Deployments, ReplicaSets & Scaling 🚀

## 📚 What I Learned

* What is a Deployment
* What is a ReplicaSet
* What is a Pod
* Replicas
* Self-healing
* Scaling Pods
* Labels and Selectors
* Deployment YAML
* Rolling Updates
* Rollbacks
* Declarative management

## 🔗 Kubernetes Relationship

```text
Deployment
    ↓
ReplicaSet
    ↓
Pods
    ↓
Containers
```

## 📄 Deployment YAML

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx-deployment

spec:
  replicas: 3

  selector:
    matchLabels:
      app: nginx

  template:
    metadata:
      labels:
        app: nginx

    spec:
      containers:
        - name: nginx
          image: nginx
```

## 🛠️ Hands-on Commands

### Create Deployment

```bash
kubectl apply -f deployment.yaml
```

### Check Deployment

```bash
kubectl get deployments
```

### Check ReplicaSet

```bash
kubectl get replicasets
```

### Check Pods

```bash
kubectl get pods
```

### Describe Deployment

```bash
kubectl describe deployment nginx-deployment
```

### Scale Up

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

### Scale Down

```bash
kubectl scale deployment nginx-deployment --replicas=2
```

### Check Rollout

```bash
kubectl rollout status deployment nginx-deployment
```

### Check Rollout History

```bash
kubectl rollout history deployment nginx-deployment
```

### Rollback

```bash
kubectl rollout undo deployment nginx-deployment
```

### Delete Deployment

```bash
kubectl delete -f deployment.yaml
```

## 🧪 Practical Tasks

* Created an Nginx Deployment with 3 replicas
* Checked Deployment, ReplicaSet and Pods
* Deleted a Pod and observed Kubernetes self-healing
* Scaled Pods from 3 → 5
* Scaled Pods from 5 → 2
* Practiced rolling updates
* Practiced rollback

## 🎯 Key Learning

**Pod** → Runs containers.

**ReplicaSet** → Maintains the desired number of Pods.

**Deployment** → Manages ReplicaSets, updates, rollbacks and scaling.

**Scaling** → Increases or decreases the number of Pods.

