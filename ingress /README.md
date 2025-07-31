# Kubernetes Ingress Controller Setup (NGINX)

This guide walks you through installing the NGINX Ingress Controller and creating a basic Ingress resource in Kubernetes.

---

## Step 1: Install the NGINX Ingress Controller

Apply the official NGINX Ingress manifest:

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.9.4/deploy/static/provider/cloud/deploy.yaml

