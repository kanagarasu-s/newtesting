# newtesting...

A simple NGINX-based web application demonstrating Docker build, CI/CD with GitHub Actions, and deployment to a remote server and Kubernetes.

## Features

- NGINX static site containerization
- Automated build, test, and Docker Hub push using GitHub Actions
- Remote server deployment via SSH
- Example Kubernetes deployment manifest

## Getting Started

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Git](https://git-scm.com/)
- (For deploy) Access to a remote server with Docker installed
- (For k8s) A running Kubernetes cluster (e.g., Minikube, k3s, or cloud provider)

### Installation & Local Run

1. **Clone the repository**
    ```sh
    git clone https://github.com/kanagrasuaws/newtesting.git
    cd newtesting
    ```

2. **Build the Docker image**
    ```sh
    docker build -t my-app .
    ```

3. **Run the Docker container**
    ```sh
    docker run -d -p 80:80 --name my-app my-app
    ```

4. **Open your browser:**  
   Visit [http://localhost](http://localhost) to see the site.

## Docker & CI/CD

- The `.github/workflows/docker-build-deploy.yml` workflow:
    - Builds the Docker image
    - Runs tests (placeholder)
    - Pushes the image to Docker Hub
    - Deploys to a remote server over SSH

**Secrets Required for CI/CD:**
- `DOCKER_USERNAME`, `DOCKER_PASSWORD`
- `SERVER_IP`, `SSH_USER`, `SSH_PRIVATE_KEY`

## Kubernetes Deployment

1. **Edit `k8s/deployment.yml`** if needed (image name, ports, etc.)
2. **Apply the manifest:**
    ```sh
    kubectl apply -f k8s/deployment.yml
    ```
3. **Access the service:**  
   If running locally (e.g., Minikube), use `minikube service myapp-service`  
   For NodePort, open `http://<node-ip>:30007/`

## Project Structure

```
.
├── dockerfile
├── index.html
├── k8s/
│   └── deployment.yml
├── .github/
│   └── workflows/
│       └── docker-build-deploy.yml
└── README.md
```

# Kubernetes Deployment with ArgoCD, Ingress, and Docker

This project demonstrates a complete CI/CD pipeline using **Docker**, **Kubernetes**, **ArgoCD**, and **NGINX Ingress Controller**.

---

## 🔧 Project Structure

| Folder/File              | Description                                   |
|--------------------------|-----------------------------------------------|
| `argocd/`                | Contains ArgoCD Application YAMLs             |
| `ingress/`               | Contains NGINX Ingress resources              |
| `k8s/`                   | Base Kubernetes manifests (deployment, svc)   |
| `Dockerfile`             | Docker image definition for the application   |
| `index.html`             | Sample web UI served by the container         |
| `README.md`              | This documentation file                       |

---

## 🚀 Prerequisites

- Kubernetes Cluster (Minikube / EKS / K3s etc.)
- `kubectl` configured
- ArgoCD installed
- NGINX Ingress Controller installed
- Docker

---

## 📦 Build & Push Docker Image

```bash
docker build -t your-dockerhub-username/your-app-name:latest .
docker push your-dockerhub-username/your-app-name:latest


## Contributing

Pull requests are welcome. For major changes, please open an issue first.

## License

[MIT](LICENSE) (or specify your license)

## Contact

Maintained by [kanagrasu-s](https://github.com/kanagrasu-s)
