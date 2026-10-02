# Kubernetes Scenario 1 – Nginx Deployment

## 🎯 Objective

Deploy an Nginx application on Kubernetes, run multiple replicas, scale the application, and expose it using a Service.

## 🛠️ Concepts Used

* Namespace
* Deployment
* ReplicaSet
* Pods
* Service
* ClusterIP
* Scaling
* Labels & Selectors

## 📌 Steps

### 1. Create Namespace

```bash
kubectl create namespace web-app
```

### 2. Create Nginx Deployment

Created an Nginx Deployment with **3 replicas**.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
  namespace: web-app
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

### 3. Scale Deployment

Scaled Nginx from **3 → 5 replicas**:

```bash
kubectl scale deployment nginx-deploy --replicas=5 -n web-app
```

### 4. Create Service

Created a **ClusterIP Service** to connect to the Nginx Pods.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-svc
  namespace: web-app
spec:
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
  type: ClusterIP
```

### 5. Test Application

Used port forwarding:

```bash
kubectl port-forward svc/nginx-svc 8080:80 -n web-app
```

Opened:

```text
http://localhost:8080
```

Nginx successfully opened in the browser.

## ✅ Result

Successfully deployed and exposed Nginx with Kubernetes.

**3 replicas → scaled to 5 replicas → Service → Browser testing**

**Status: Completed ✅**
