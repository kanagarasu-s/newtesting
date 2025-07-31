# Argo CD Setup via GitHub on Linux

This guide explains how to set up Argo CD in a Kubernetes cluster and connect it to a GitHub repository using GitOps practices.

## Prerequisites

- Kubernetes cluster (Minikube, EKS, GKE, etc.)
- `kubectl` installed
- `helm` (optional)
- `argocd` CLI (optional)
- GitHub repository with Kubernetes manifests or Helm charts

## Steps

### 1. Install Argo CD

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### 2. Expose the Argo CD API Server

**Option A: Port forward**

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

**Option B: LoadBalancer**

```bash
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

### 3. Get the Initial Admin Password

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

### 4. Install Argo CD CLI

```bash
VERSION=$(curl -s https://api.github.com/repos/argoproj/argo-cd/releases/latest | grep tag_name | cut -d '"' -f 4)
curl -sSL -o argocd "https://github.com/argoproj/argo-cd/releases/download/${VERSION}/argocd-linux-amd64"
chmod +x argocd
sudo mv argocd /usr/local/bin
```

### 5. Login to Argo CD CLI

```bash
argocd login localhost:8080 --username admin --password <copied-password> --insecure
```

### 6. Connect Argo CD to GitHub

**Option A: Use YAML definition**

Apply `argocd-application.yaml` using `kubectl`:

```bash
kubectl apply -f argocd-application.yaml
```

**Option B: Use CLI**

```bash
argocd app create my-app \
  --repo https://github.com/YOUR_USERNAME/YOUR_REPO.git \
  --path k8s/app1 \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace default \
  --sync-policy automated
```

## Notes

- Keep GitHub repo updated with your manifests
- Use `argocd app sync my-app` to trigger a manual sync
- Integrate GitHub webhook for auto-sync (optional)
