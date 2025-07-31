Create Argo CD via GitHub on Linux
Prerequisites
✅ A running Kubernetes cluster (like Minikube, EKS, GKE, etc.)
✅ kubectl installed and configured
✅ helm installed (optional but useful)
✅ argocd CLI installed (optional but helpful)
✅ A GitHub repository with your Kubernetes YAML manifests (or Helm charts)
Step 1: Install Argo CD
Create namespace: kubectl create namespace argocd
Install manifests: kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
Step 2: Expose Argo CD API Server
Option A: Port forward: kubectl port-forward svc/argocd-server -n argocd 8080:443
Option B: LoadBalancer: kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
Step 3: Get Initial Admin Password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
Step 4: Install Argo CD CLI
VERSION=$(curl -s https://api.github.com/repos/argoproj/argo-cd/releases/latest | grep tag_name | cut -d '"' -f 4)
curl -sSL -o argocd "https://github.com/argoproj/argo-cd/releases/download/${VERSION}/argocd-linux-amd64"
chmod +x argocd && sudo mv argocd /usr/local/bin
Step 5: Login via CLI
argocd login localhost:8080 --username admin --password <copied-password> --insecure
Step 6: Connect to Your GitHub Repo
Option A: Use Kubernetes YAML Application (app.yaml) and apply using kubectl
Option B: Use argocd CLI to create application
Final Notes
Update your GitHub repo with manifests regularly.
Use argocd app sync my-app to force a manual sync.
