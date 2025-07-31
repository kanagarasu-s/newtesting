# Kubernetes Ingress Controller Setup (NGINX)

This guide walks you through installing the NGINX Ingress Controller and creating a basic Ingress resource in Kubernetes.

---

## Step 1: Install the NGINX Ingress Controller

Apply the official NGINX Ingress manifest:

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.9.4/deploy/static/provider/cloud/deploy.yaml
Wait for all pods in the ingress-nginx namespace to be ready:

kubectl get pods -n ingress-nginx
## Step 2: Verify the Ingress Controller Service

Check if the controller service is exposed:
kubectl get svc -n ingress-nginx

For cloud environments, look for a LoadBalancer external IP.

For Minikube or bare metal, use NodePort or port-forwarding.

## Step 3: Create an Example Application
Run the following commands to deploy a sample app and expose it as a service:

bash
Copy
Edit
kubectl create deployment my-app --image=httpd
kubectl expose deployment my-app --port=80 --target-port=80
