# Kubernetes Installation using kubeadm (YUM-based Linux)

This guide helps you install Kubernetes (v1.28) using `kubeadm` on a Linux system with Docker and Calico CNI.

---

## Step-by-Step Instructions

### Step 1: Install Docker

```bash
yum install docker -y
systemctl enable docker && systemctl start docker
```

### Step 2: Disable Swap

```bash
swapoff -a
```

To make swap permanently off, edit `/etc/fstab` and comment out the swap line.

---

### Step 3: Set Docker Cgroup Driver

Edit Docker daemon configuration:

```bash
vi /etc/docker/daemon.json
```

Add the following:

```json
{
  "exec-opts": ["native.cgroupdriver=systemd"]
}
```

Then restart Docker:

```bash
sudo systemctl restart docker
```

---

### Step 4: Add Kubernetes Repo

```bash
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.28/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.28/rpm/repodata/repomd.xml.key
exclude=kubelet kubeadm kubectl cri-tools kubernetes-cni
EOF
```

---

### Step 5: Configure Kernel Parameters

```bash
cat <<EOF > /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF

sysctl --system
```

---

### Step 6: Disable SELinux Temporarily

```bash
setenforce 0
```

To disable it permanently, update `/etc/selinux/config` and set `SELINUX=permissive`.

---

### Step 7: Install Kubernetes Components

```bash
yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
systemctl enable kubelet && systemctl start kubelet
```

---

### Step 8: Initialize Kubernetes Cluster

On the **master node only**:

```bash
kubeadm init
```

After success, run the below to start using `kubectl`:

```bash
export KUBECONFIG=/etc/kubernetes/admin.conf
```

(You can add this line to your `.bashrc` for persistence.)

---

### Step 9: Install Calico CNI

```bash
kubectl --kubeconfig=/etc/kubernetes/admin.conf apply -f https://docs.projectcalico.org/v3.15/manifests/calico.yaml
```

---

## Step 10: Join Worker Nodes (Run on Workers)

Copy and run the join command shown after `kubeadm init`, for example:

```bash
kubeadm join <MASTER_IP>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

---

## Step 11: Verify Cluster

```bash
kubectl get nodes
kubectl get pods -A
```

---

✅ Done! Kubernetes is now running using kubeadm with Docker and Calico CNI.

