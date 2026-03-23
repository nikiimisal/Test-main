🚀 FINAL DEPLOYMENT (Ubuntu + kubeadm + Terraform + Helm)
🟢 STEP 1: Launch EC2 Instance

👉 Go to: Amazon Web Services

Configure:
Name: monitoring-server
AMI: Ubuntu 22.04 ✅
Instance: t3.small (min) / t3.medium (better)
Key pair: .pem
🔥 Security Group

Allow:

22 → SSH
3000 → Grafana
9090 → Prometheus
6443 → Kubernetes
🟢 STEP 2: Connect to EC2
ssh -i your-key.pem ubuntu@<EC2-PUBLIC-IP>
🟢 STEP 3: Create Setup Script
nano k8s-common.sh
👉 Paste THIS (Final Working Script 🔥)
#!/bin/bash
set -e

echo "===== Kubernetes Setup Started ====="

# Disable swap
sudo swapoff -a
sudo sed -i '/ swap / s/^/#/' /etc/fstab

# Load kernel modules
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF

sudo modprobe overlay
sudo modprobe br_netfilter

# Sysctl settings
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables=1
net.bridge.bridge-nf-call-ip6tables=1
net.ipv4.ip_forward=1
EOF

sudo sysctl --system

# Install containerd
sudo apt update
sudo apt install -y containerd

sudo mkdir -p /etc/containerd
containerd config default | sudo tee /etc/containerd/config.toml
sudo sed -i 's/SystemdCgroup = false/SystemdCgroup = true/' /etc/containerd/config.toml

sudo systemctl restart containerd
sudo systemctl enable containerd

echo "Containerd Installed"

# Install Kubernetes tools
sudo apt-get update -y
sudo apt-get install -y apt-transport-https ca-certificates curl gpg

sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.29/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.29/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update -y
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl

echo "Kubernetes Installed"
🟢 STEP 4: Run Script
chmod +x k8s-common.sh
./k8s-common.sh
🟢 STEP 5: Initialize Kubernetes
sudo kubeadm init --pod-network-cidr=10.244.0.0/16

👉 ⚠️ End ला command येईल → ignore for now

🟢 STEP 6: Configure kubectl
mkdir -p $HOME/.kube
sudo cp /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown ubuntu:ubuntu $HOME/.kube/config
🟢 STEP 7: Install Network Plugin
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
🟢 STEP 8: Allow Pods on Master
kubectl taint nodes --all node-role.kubernetes.io/control-plane-
🟢 STEP 9: Verify Cluster
kubectl get nodes

👉 STATUS = Ready ✔

🟢 STEP 10: Install Helm

👉 Helm

curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
🟢 STEP 11: Install Terraform

👉 Terraform

sudo apt install -y gnupg software-properties-common

wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp.gpg

echo "deb [signed-by=/usr/share/keyrings/hashicorp.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update && sudo apt install terraform -y
🟢 STEP 12: Create Project Folder
mkdir monitoring-project
cd monitoring-project
🟢 STEP 13: Create Terraform Files
touch provider.tf namespace.tf prometheus.tf grafana.tf variables.tf outputs.tf

👉 (तुझं prepared code paste कर ✔)

🟢 STEP 14: Run Terraform
terraform init
terraform apply --auto-approve
🟢 STEP 15: Verify Pods
kubectl get pods -n monitoring
🟢 STEP 16: Access Prometheus
kubectl port-forward svc/prometheus-server 9090:80 -n monitoring --address 0.0.0.0

👉 Open:

http://<EC2-PUBLIC-IP>:9090
🟢 STEP 17: Access Grafana
kubectl port-forward svc/grafana 3000:80 -n monitoring --address 0.0.0.0

👉 Open:

http://<EC2-PUBLIC-IP>:3000
🟢 STEP 18: Get Password
kubectl get secret --namespace monitoring grafana \
-o jsonpath="{.data.admin-password}" | base64 --decode
🧠 FINAL FLOW

👉 EC2 (Ubuntu) → containerd → kubeadm → Kubernetes → Helm → Terraform → Prometheus → Grafana
