# 🚀 Kubernetes Web App Deployment

A simple Kubernetes project where I deployed a custom HTML website using **Kubernetes Deployment, Service, Namespace, ConfigMap, Volume, and VolumeMount**.

The application runs on an **Nginx container** and is accessible through a web browser.

## 🛠️ Technologies Used

* Kubernetes
* Docker
* Nginx
* kubectl
* kind
* YAML
* ConfigMap

## 📁 Project Structure

```text
kubernetes-web-app/
│
├── namespace.yaml
├── deployment.yaml
├── service.yaml
│
└── k8s-html-project/
    └── index.html
```

## 🏗️ Kubernetes Architecture

```text
Browser
   ↓
Service
   ↓
Nginx Pods
   ↑
Deployment
   ↑
Namespace

ConfigMap
   ↓
Volume
   ↓
VolumeMount
   ↓
Nginx HTML Directory
```

## 📌 Kubernetes Resources

### 1. Namespace

Created a dedicated namespace called `web-app` to keep all project resources organized.

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: web-app
```

### 2. Deployment

Created an Nginx Deployment with **3 replicas**.

The Deployment manages the Pods and automatically creates replacement Pods if a Pod fails.

```text
Deployment
    ↓
Pod 1
Pod 2
Pod 3
```

### 3. Service

Created a NodePort Service to expose the Nginx application.

The Service selects Pods using the label:

```yaml
app: nginx
```

For local kind testing, I accessed the application using:

```bash
kubectl port-forward service/nginx-service 8080:80 -n web-app
```

Then opened:

```text
http://localhost:8080
```

### 4. ConfigMap

Stored the custom `index.html` file in a Kubernetes ConfigMap.

```bash
kubectl create configmap website-html \
  --from-file=./index.html \
  -n web-app
```

The ConfigMap allows the HTML content to be managed separately from the Nginx container image.

### 5. Volume & VolumeMount

Mounted the ConfigMap inside the Nginx container:

```text
ConfigMap
    ↓
Volume
    ↓
VolumeMount
    ↓
/usr/share/nginx/html
```

This allows Nginx to serve my custom HTML page.

## 🚀 Deployment Steps

### Step 1: Create Namespace

```bash
kubectl apply -f namespace.yaml
```

### Step 2: Create ConfigMap

```bash
kubectl create configmap website-html \
  --from-file=./k8s-html-project/index.html \
  -n web-app
```

### Step 3: Deploy Application

```bash
kubectl apply -f deployment.yaml
```

### Step 4: Create Service

```bash
kubectl apply -f service.yaml
```

### Step 5: Check Resources

```bash
kubectl get all -n web-app
```

### Step 6: Access Application

```bash
kubectl port-forward service/nginx-service 8080:80 -n web-app
```

Open:

```text
http://localhost:8080
```

## 🧪 Kubernetes Operations Practiced

### Scaling

Scaled the application from 3 Pods to 5:

```bash
kubectl scale deployment nginx-deployment --replicas=5 -n web-app
```

Scaled it back to 2:

```bash
kubectl scale deployment nginx-deployment --replicas=2 -n web-app
```

### Self-Healing

Deleted a Pod manually:

```bash
kubectl delete pod <pod-name> -n web-app
```

The Deployment automatically created a new Pod.

This demonstrates Kubernetes **self-healing**.

### Service Troubleshooting

Checked Service endpoints:

```bash
kubectl get endpoints nginx-service -n web-app
```

I also intentionally changed the Service selector and observed that the Service had no endpoints. After fixing the selector, the Pods became available again.

### Updating the Application

Updated the HTML content and recreated the ConfigMap:

```bash
kubectl create configmap website-html \
  --from-file=./k8s-html-project/index.html \
  -n web-app \
  --dry-run=client -o yaml | kubectl apply -f -
```

Restarted the Deployment:

```bash
kubectl rollout restart deployment nginx-deployment -n web-app
```

Checked rollout status:

```bash
kubectl rollout status deployment nginx-deployment -n web-app
```

## 🔍 Useful Commands

Check Pods:

```bash
kubectl get pods -n web-app
```

Check Deployment:

```bash
kubectl get deployment -n web-app
```

Check Service:

```bash
kubectl get service -n web-app
```

Check ConfigMap:

```bash
kubectl get configmap -n web-app
```

Describe a Pod:

```bash
kubectl describe pod <pod-name> -n web-app
```

View Pod logs:

```bash
kubectl logs <pod-name> -n web-app
```

Check Deployment rollout:

```bash
kubectl rollout status deployment nginx-deployment -n web-app
```

## 🎯 What I Learned

Through this project, I practiced:

* Creating and managing Kubernetes Namespaces
* Deploying applications using Deployments
* Managing multiple Pod replicas
* Exposing applications using Services
* Using Labels and Selectors
* Creating and using ConfigMaps
* Using Volumes and VolumeMounts
* Kubernetes self-healing
* Scaling applications
* Troubleshooting Services and Pods
* Performing application updates
* Accessing a Kubernetes application from a browser
* Working with Kubernetes using `kubectl`
* Running Kubernetes locally using kind

## 💡 Project Outcome

Successfully deployed a custom HTML website on **Kubernetes + Nginx** and accessed it through a browser.

The project demonstrates fundamental Kubernetes concepts that are important for a **DevOps Engineer** role.

## 👨‍💻 Author

**Sanjit Bhagat**

Aspiring DevOps Engineer

Skills: Linux | Git | Docker | AWS | Kubernetes | Terraform
