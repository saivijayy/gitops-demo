# 🚀 GitOps Workflow with ArgoCD and Kubernetes

This project implements a GitOps workflow using **ArgoCD** to automatically deploy a sample NGINX application to a Kubernetes cluster (Minikube) from a GitHub repository.

---

## 📌 Objectives

- Deploy and configure **ArgoCD** on Kubernetes
- Push Kubernetes manifests to GitHub
- Use ArgoCD to auto-sync deployments from the Git repo
- Demonstrate GitOps by triggering deployments via Git commits

---

## ⚙️ Tech Stack

- Kubernetes (Minikube)
- ArgoCD
- Docker
- GitHub
- NGINX (sample app)

---

## 📁 Project Structure

gitops-task/ └── k8s-manifests/ ├── deployment.yaml # NGINX deployment └── service.yaml # NodePort service

---

## 🚀 Setup & Usage

### 1. Start Minikube

```bash
minikube start
```
### 2. Install ArgoCD
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
### 3. Access ArgoCD UI
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
# Open: http://localhost:8080
### Default username: 
```bash
admin
```
### Get password:
```bash
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d
```
### 4. Deploy NGINX via ArgoCD
Create app in ArgoCD UI:

Git repo: https://github.com/saivijayy/gitops-demo

Path: k8s-manifests

Auto-Sync: ✅ Enabled

ArgoCD will pull manifests and deploy automatically.

### 5. Expose NGINX app
```bash
minikube service nginx-service
```
### 6. 🔁 GitOps in Action
```bash
Change version/tag in deployment.yaml

Commit & push to GitHub
```
### ArgoCD syncs automatically → pod updated!

✅ Updated Section: Access NGINX using Minikube
markdown
Copy
Edit
### 7. 🌐 Accessing NGINX App via Minikube

After ArgoCD deploys the NGINX app, you can expose and access it using Minikube:

### 8. Check if the service is running

```bash
kubectl get svc nginx-service
```
### 9. You should see something like:
```pgsql
NAME            TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
nginx-service   NodePort   10.96.34.121   <none>        80:30544/TCP   5m
```
### 10. Access the NGINX service using Minikube
```bash
minikube service nginx-service
```

### This will:

Start a tunnel to expose the NodePort

Open the default browser (or show the URL like http://127.0.0.1:33171)

Allow you to view the running NGINX homepage

### Example output:
```pgsql
🏃  Starting tunnel for service nginx-service.
|-----------|---------------|-------------|------------------------|
| NAMESPACE |     NAME      | TARGET PORT |          URL           |
|-----------|---------------|-------------|------------------------|
| default   | nginx-service |          80 | http://127.0.0.1:33171 |
```
### 📄 Resume Line
Implemented GitOps pipeline using ArgoCD and Kubernetes to automate app deployment from GitHub to a Kubernetes cluster.

### ✍️ Author
Sai Vijay
