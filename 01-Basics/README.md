# Kubernetes Day 1 🚀

## What I Learned

Today I started learning Kubernetes for DevOps.

### Topics Covered

* What is Kubernetes?
* Why Kubernetes is used
* Kubernetes Cluster
* Control Plane
* Worker Node
* Kubernetes Architecture
* API Server
* etcd
* Scheduler
* Controller Manager
* Kubelet
* Kube-proxy
* Container Runtime
* Pods
* Namespaces
* Basic `kubectl` commands

## Tools Used

* Docker Desktop
* Kubernetes
* kubectl
* kind

## Hands-on Practice

### Create Kubernetes Cluster

```bash
kind create cluster --name devops-cluster
```

### Check Cluster

```bash
kubectl cluster-info
```

### Check Nodes

```bash
kubectl get nodes
```

### Check Pods

```bash
kubectl get pods
```

### Create Nginx Pod

```bash
kubectl run nginx --image=nginx
```

### Get Pod Details

```bash
kubectl get pods -o wide
```

### Describe Pod

```bash
kubectl describe pod nginx
```

### Check Logs

```bash
kubectl logs nginx
```

### Enter Container

```bash
kubectl exec -it nginx -- bash
```

### Port Forwarding

```bash
kubectl port-forward pod/nginx 8080:80
```

### Delete Pod

```bash
kubectl delete pod nginx
```

## Day 1 Goal

Understand Kubernetes fundamentals and create my first Kubernetes cluster and Pod using **kind**.

## Next

➡️ Day 2: Kubernetes YAML and Pod configuration.
