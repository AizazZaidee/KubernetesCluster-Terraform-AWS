
# Terraform & Kubernetes Setup on AWS

This repository provides a complete solution for deploying a Kubernetes cluster on AWS using EC2 instances. It uses Terraform for infrastructure provisioning and a set of Bash scripts to configure the instances and install Kubernetes components.

## Architecture Overview

The setup includes the following:

- **Master Node**: The control plane of the Kubernetes cluster.
- **Worker Node**: A node that will join the Kubernetes cluster as a worker.
- **IAM Role & Instance Profile**: Permissions are provided for EC2 instances to interact with other AWS services like EC2 Instance Connect.
- **Security Group**: A security group that allows SSH, HTTP, and custom Kubernetes ports.
- **EC2 Instance Connect**: SSH key management via AWS EC2 Instance Connect, which simplifies secure SSH access without needing to manage private keys.

## Prerequisites

Before running the Terraform code, make sure you have the following:

1. **AWS CLI** installed and configured with necessary IAM permissions.
2. **Terraform** installed.
3. An existing **AWS EC2 Keypair** (replace `<<keyPairName>>` with your keypair name).
4. **Kubernetes** knowledge to understand the setup and usage.

## Usage

### 1. Clone the Repository
```bash
git clone https://github.com/AizazZaidee/KubernetesCluster-Terraform-AWS.git
cd KubernetesCluster-Terraform-AWS
```

### 2. Update Variables
Edit the `locals` block in `main.tf` to update the following variables:

- `keyname`: The name of your existing AWS EC2 Keypair.
- `region`: The AWS region in which the resources will be created (default is `us-west-2`).
- `ami`: The AMI ID for your EC2 instances (the one used in this example is for Ubuntu 20.04).

### 3. Apply Terraform Configuration
Run the following commands to provision the resources:

```bash
terraform init
terraform plan
terraform apply
```

### 4. SSH Access to Master Node
After Terraform applies, you can access the master node using the following command:

```bash
ssh -i /path/to/your/keypair.pem ubuntu@<master_public_ip>
```

### 5. Worker Node Join
The worker node will automatically join the Kubernetes cluster once it’s up and running. You can verify its status with:

```bash
kubectl get nodes
```

### 6. Output
The `master_public_dns` and `worker_public_dns` outputs will give you the public DNS of both the master and worker nodes.

## What’s Included

### 1. **Terraform Configuration**
The Terraform code provisions:

- EC2 instances for both the master and worker nodes.
- IAM roles and policies for secure communication between EC2 instances.
- Security groups for network access.

### 2. **User Data Script (`master.sh` and `worker.sh`)**
Bash scripts to:

- Install Kubernetes components (kubelet, kubeadm, kubectl).
- Configure Docker and containerd.
- Set up the worker node to join the master node automatically using EC2 Instance Connect.

### 3. **IAM Role Policy**
An IAM role with the policy `ec2-instance-connect:SendSSHPublicKey` to allow the worker node to connect to the master node using EC2 Instance Connect.

## Contributing

Feel free to fork, clone, and contribute to this repository! If you find any issues or have suggestions for improvements, please create an issue or pull request.
