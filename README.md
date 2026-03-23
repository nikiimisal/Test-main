#  



## 📌 PROJECT OVERVIEW

THIS PROJECT SETS UP A COMPLETE MONITORING STACK USING:

- KUBERNETES (KUBEADM)
- CONTAINERD
- HELM
- TERRAFORM
- PROMETHEUS 📊
- GRAFANA 📈

# PROJECT STRUCTURE

Create a folder `monitoring-project`:

```
monitoring-project/
├── provider.tf
├── namespace.tf
├── prometheus.tf
├── grafana.tf
├── variables.tf
├── outputs.tf
```




##🔹 STEP 0: PREREQUISITES

Make sure your environment has:

- Terraform installed → `terraform -v` ⚡
- kubectl installed & configured → `kubectl get nodes` ☸️
- Helm installed → `helm version` ⛵
- A Kubernetes cluster ready (your EC2 node as a single-node cluster is fine)
- Enough RAM (at least 4GB) for Prometheus 📊 + Grafana 📈

---





## 🔹 STEP 1: LAUNCH EC2 INSTANCE

AWS → EC2 → Launch

- **Name:** `monitoring-server`
- **AMI:** `Ubuntu 22.04 LTS`
- **Instance Type:** `t3.medium` (minimum) / `t3.large` (recommended)
- **Key Pair:** `.pem`
- **Security Group:**
  - `22 → SSH`
  - `3000 → Grafana` 
  - `9090 → Prometheus` 
  - `6443 → Kubernetes API` 

> In this project, we are not launching separate servers for the master and worker nodes. Both the control plane (master) and worker components run on the same server.


## 🔹 STEP 2: Connect to EC2

Use SSH to connect to your instance:

```bash
ssh -i your-key.pem ubuntu@<EC2-Public-IP>
```



##  🔹 STEP 3: Create Kubernetes Setup Script

Create a script file for Kubernetes setup:

```
sudo nano k8s-common.sh
```
- IF you using

For ubuntu : [click here](https://github.com/nikiimisal/Internship__Project-4__Raw-material/blob/main/k8s-common.sh)
For Amazon : [click here](https://github.com/nikiimisal/Internship__Project-4__Raw-material/blob/main/k8s-common.sh%20%20(1))



>We are using Ubuntu, so commands are Ubuntu-specific. For Amazon Linux, some commands may differ.
>Make sure the OS supports a command before running it.


##  🔹 STEP 4: Run Setup Script

```
sudo chmod +x k8s-common.sh
sudo ./k8s-common.sh
```

##  🔹 STEP 5: Initialize Kubernetes

```
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

##  🔹 STEP 6: Configure kubectl

```Bash
mkdir -p $HOME/.kube
sudo cp /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown ubuntu:ubuntu $HOME/.kube/config
```


## 🔹 STEP 7: Install Network Plugin (Flannel)

```Bash
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

##  🔹 STEP 8: Allow Pods on Master

```Bash
kubectl taint nodes --all node-role.kubernetes.io/control-plane-
```

##  🔹 STEP 9: Verify Cluster

```
kubectl get nodes
```
STATUS should be: Ready ✔



##  🔹 STEP 10: Install Helm

```
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

##  🔹 STEP 11: Install Terraform

```Bash
sudo apt install -y gnupg software-properties-common
wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update
sudo apt install terraform -y
```

##  🔹 STEP 12: Create Project Folder

```
mkdir monitoring-project
cd monitoring-project
```

##  🔹 STEP 13: Create Terraform Files

```Bash
touch provider.tf namespace.tf prometheus.tf grafana.tf variables.tf outputs.tf
```
Paste your prepared Terraform + Helm code into these files.

>To see files [click here](https://github.com/nikiimisal/Internship__Project-4__Raw-material)



##  🔹 STEP 14: Run Terraform

```Bash
terraform init
terraform plan   # if you wan see your plane
terraform apply --auto-approve
```

- Terraform will deploy:

  - Monitoring namespace
  - Prometheus
  - Grafana


##   🔹 STEP 15: Verify Pods

```Bash
kubectl get pods -n monitoring
```

##  🔹 STEP 16: Access Prometheus


```Bash
kubectl port-forward svc/prometheus-server 9090:80 -n monitoring --address 0.0.0.0
```

If you want to run it on the backend, use this command.
```Bash
nohup kubectl port-forward svc/prometheus-server 9090:80 -n monitoring --address 0.0.0.0 > prometheus_pf.log 2>&1 &
```
Open browser:

```
http://<EC2-Public-IP>:9090
```



##  🔹 STEP 17: Access Grafana

```
kubectl port-forward svc/grafana 3000:80 -n monitoring --address 0.0.0.0
```

If you want to run it on the backend, use this command.
```Bash
nohup kubectl port-forward svc/grafana 3000:80 -n monitoring --address 0.0.0.0 > grafana_pf.log 2>&1 &
```

Open browser:
```
http://<EC2-Public-IP>:3000
```


##  🔹 STEP 18: Get Grafana Password

```Bash
kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode
```

Username: `admin`
Password: output of the above command


##  ✅ FINAL FLOW

```
EC2 → containerd → kubeadm → Kubernetes → Helm → Terraform → Prometheus → Grafana
```




























