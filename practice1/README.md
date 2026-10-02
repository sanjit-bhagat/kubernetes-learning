# Kubernetes Scenario 2 – ConfigMap

## 🎯 Objective

Use a Kubernetes ConfigMap to store application configuration and pass it to a Pod as an environment variable.

## 🛠️ Concepts Used

* ConfigMap
* Deployment
* Environment Variables
* `configMapKeyRef`

## 📌 Steps

### 1. Create ConfigMap

Created a ConfigMap named `app-config`.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
  namespace: web-app

data:
  APP_NAME: shopping-cart
  APP_ENV: production
  APP_PORT: "5000"
  LOG_LEVEL: info
```

Apply:

```bash
kubectl apply -f configmap.yaml
```

### 2. Use ConfigMap in Deployment

Imported only the `LOG_LEVEL` value into the Nginx container.

```yaml
env:
  - name: LOG_LEVEL
    valueFrom:
      configMapKeyRef:
        name: app-config
        key: LOG_LEVEL
```

### 3. Verify

Check the Pod:

```bash
kubectl get pods -n web-app
```

Check the environment variable:

```bash
kubectl exec -it <pod-name> -n web-app -- env
```

Expected:

```text
LOG_LEVEL=info
```

## 🧠 Key Learning

* `ConfigMap` stores non-sensitive application configuration.
* `envFrom` can import all ConfigMap values.
* `configMapKeyRef` can import a specific ConfigMap value.
* ConfigMap keeps configuration separate from application code.

## ✅ Result

Successfully created a ConfigMap and injected a specific configuration value into a Kubernetes Pod.

**Status: Completed ✅**
