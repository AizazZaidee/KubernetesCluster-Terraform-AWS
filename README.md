# 🚀 Terraform & Kubernetes Setup on AWS 🎯

Welcome to this **awesome** repository! 🎉 Here, you’ll find a complete solution to deploy a **Kubernetes cluster** on AWS using **EC2 instances**—all powered by Terraform & Bash scripts! ⚡

---

## 🌍 Architecture Overview

Here’s what this setup includes:

- **🛠️ Master Node**: The **control center** of your Kubernetes cluster.
- **🚜 Worker Node**: The **heavy lifter** that joins the cluster and runs workloads.
- **🔐 IAM Role & Instance Profile**: Secure permissions for EC2 instances to interact with AWS services.
- **🛡️ Security Group**: Controls access via **SSH, HTTP, and Kubernetes ports**.
- **🔑 EC2 Instance Connect**: Securely manage SSH keys—no more private key headaches! 😎

---

## ✅ Prerequisites

Before diving in, ensure you have the following installed and configured:

1. **AWS CLI** 🏗️ – Installed and configured with proper IAM permissions.
2. **Terraform** ⛏️ – Installed and ready to go!
3. **AWS EC2 Keypair** 🔑 – Create one and replace `<<keyPairName>>` in the config.
4. **Kubernetes knowledge** 📚 – A basic understanding will help!

---

## 🚀 Usage

### 1️⃣ Clone the Repository 🌀
```bash
 git clone https://github.com/AizazZaidee/KubernetesCluster-Terraform-AWS.git
 cd KubernetesCluster-Terraform-AWS
```

### 2️⃣ Update Variables ✏️
Modify the `locals` block in `main.tf` to update:

- `keyname`: Your **AWS EC2 Keypair name**.
- `region`: AWS region (default: `us-west-2`).
- `ami`: **Ubuntu 20.04 AMI ID** (or another of your choice).

### 3️⃣ Deploy with Terraform ⚡
Run these magic commands to **bring your cluster to life**:
```bash
terraform init
terraform plan
terraform apply
```

### 4️⃣ Access the Master Node 🖥️
Once deployed, SSH into the master node:
```bash
ssh -i /path/to/your/keypair.pem ubuntu@<master_public_ip>
```

### 5️⃣ Verify Worker Node 🏗️
Your **worker node** will automatically join the cluster! Verify with:
```bash
kubectl get nodes
```

### 6️⃣ Outputs 📜
Terraform will display the **public DNS names** of your master and worker nodes. Use them to access your instances easily!

---

## 🎁 What’s Included?

### 🏗️ **Terraform Configuration**
Terraform sets up:
- **EC2 instances** (Master & Worker)
- **IAM Roles & Policies** for security
- **Security Groups** for controlled access

### 📝 **User Data Scripts (`master.sh` & `worker.sh`)**
These **Bash scripts**:
- Install Kubernetes components (**kubelet, kubeadm, kubectl**)
- Configure **Docker & containerd**
- Ensure the worker node **auto-joins** the cluster 🎯

### 🔑 **IAM Role Policy**
The IAM role allows secure **SSH access** via EC2 Instance Connect—no need to manage SSH keys manually! 🔥

---

## 🤝 Contributing

Found a bug? 🐞 Have an idea? 💡 **Fork**, **clone**, and contribute! Feel free to open an **issue** or **pull request**. Let’s make this repo even better! 🚀

Happy Deploying! 🎉✨

