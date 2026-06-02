# 🚀 3-Tier Web Application Deployment on Kubernetes using AWS & DevOps
# 🎥 Project Demonstration 

https://github.com/user-attachments/assets/6c0db189-c3e2-4674-833d-1e99ff8d6a95

https://github.com/user-attachments/assets/94576cae-4fad-4908-8a36-d0b5a0ecc83e

## 📌 Project Overview

This project demonstrates the deployment of a **Three-Tier Web Application** using **Docker, Kubernetes, AWS, and GitHub Actions CI/CD Pipeline**.

The application is divided into three layers:

* **Frontend Layer** → ReactJS
* **Backend Layer** → NodeJS & ExpressJS
* **Database Layer** → MongoDB

The project focuses on implementing modern DevOps practices including:

* Containerization using Docker
* Kubernetes orchestration
* CI/CD automation with GitHub Actions
* Cloud deployment on AWS
* Scalable and production-ready architecture

---

# 🏗️ Architecture

```text id="0xj4sv"
                User
                  │
                  ▼
        Frontend (ReactJS)
                  │
                  ▼
       Backend API (NodeJS)
                  │
                  ▼
         MongoDB Database
```

---

# 📂 Repository Structure

```bash id="qz7eq0"
3-tier-web-app-Kubernetes/
│
├── .github/workflows/
│   └── deploy.yml
│
├── Application-Code/
│   ├── frontend/
│   ├── backend/
│   └── database/
│
├── Kubernetes-Manifests-file/
│   ├── frontend-deployment.yml
│   ├── backend-deployment.yml
│   ├── mongo-deployment.yml
│   ├── services.yml
│
├── .gitignore
└── README.md
```

---

# 🛠️ Technologies Used

| Technology     | Purpose                 |
| -------------- | ----------------------- |
| AWS EC2        | Cloud Hosting           |
| Docker         | Containerization        |
| Kubernetes     | Container Orchestration |
| GitHub Actions | CI/CD Pipeline          |
| ReactJS        | Frontend                |
| NodeJS         | Backend                 |
| MongoDB        | Database                |
| Git            | Version Control         |

---

# ⚙️ Prerequisites

Before starting, install the following:

* AWS Account
* GitHub Account
* Docker
* Kubernetes Cluster
* kubectl
* AWS CLI

---

# ☁️ AWS EC2 Setup

## Step 1: Launch EC2 Instance

* Open AWS Console
* Launch Ubuntu EC2 Instance
* Configure Security Group

Allow these inbound ports:

| Port | Purpose            |
| ---- | ------------------ |
| 22   | SSH                |
| 80   | HTTP               |
| 3000 | Frontend           |
| 5000 | Backend            |
| 6443 | Kubernetes API     |
| 8080 | Jenkins (Optional) |

---

## Step 2: Connect to EC2

```bash id="c63j1z"
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```

---

# 🐳 Install Docker

## Update Packages

```bash id="i8mjlwm"
sudo apt update
```

## Install Docker

```bash id="6u1vx0"
sudo apt install docker.io -y
```

## Start Docker

```bash id="0b21jr"
sudo systemctl start docker
sudo systemctl enable docker
```

## Add User to Docker Group

```bash id="up6q2n"
sudo usermod -aG docker ubuntu
newgrp docker
```

## Verify Docker Installation

```bash id="78it3x"
docker --version
```

---

# ☸️ Install Kubernetes Tools

## Install kubectl

```bash id="a4zphm"
curl -LO "https://dl.k8s.io/release/$(curl -L -s \
https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

```bash id="chf3ks"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

## Verify kubectl

```bash id="4a4w9k"
kubectl version --client
```

---

# 📥 Clone Repository

```bash id="fth5b7"
git clone https://github.com/ImDamandeepKaur/3-tier-web-app-Kubernetes.git
```

```bash id="grm6lx"
cd 3-tier-web-app-Kubernetes
```

---

# 🐳 Build Docker Images

## Frontend

```bash id="o8m2bx"
cd Application-Code/frontend
docker build -t frontend-app .
```

## Backend

```bash id="0z5bff"
cd ../backend
docker build -t backend-app .
```

---

# ☸️ Kubernetes Deployment

## Apply Kubernetes Manifests

```bash id="cyw5ly"
kubectl apply -f Kubernetes-Manifests-file/
```

## Verify Deployments

```bash id="w6xgcb"
kubectl get pods
```

```bash id="ev62g6"
kubectl get svc
```

---

# 🌐 Access Application

## Frontend URL

```text id="8mkrq2"
http://<EC2-PUBLIC-IP>:3000
```

## Backend URL

```text id="bnx6ru"
http://<EC2-PUBLIC-IP>:5000
```

---

# 🔄 CI/CD Pipeline using GitHub Actions

The project uses GitHub Actions for automated deployment.

## Workflow Location

```text id="dbbmbv"
.github/workflows/
```

---

# 🔐 GitHub Secrets Configuration

Go to:

```text id="1sxyi1"
Repository → Settings → Secrets and Variables → Actions
```

Add:

| Secret Name  | Description     |
| ------------ | --------------- |
| EC2_HOST     | EC2 Public IP   |
| EC2_USERNAME | ubuntu          |
| EC2_SSH_KEY  | Private SSH Key |

---

# 📄 GitHub Actions Workflow Example

```yaml id="1z1n67"
name: Deploy Application

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Deploy to EC2
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.EC2_HOST }}
          username: ${{ secrets.EC2_USERNAME }}
          key: ${{ secrets.EC2_SSH_KEY }}
          script: |
            cd 3-tier-web-app-Kubernetes
            git pull origin main
            kubectl apply -f Kubernetes-Manifests-file/
```

---

# 📊 Useful Kubernetes Commands

## Get Pods

```bash id="v3y7k1"
kubectl get pods
```

## Get Services

```bash id="o6l4ql"
kubectl get svc
```

## Describe Pod

```bash id="a6yjj3"
kubectl describe pod pod-name
```

## Check Logs

```bash id="fjlwmx"
kubectl logs pod-name
```

## Delete Deployment

```bash id="8hmr3x"
kubectl delete -f Kubernetes-Manifests-file/
```

---

# 🧪 Troubleshooting

## Docker Permission Denied

```bash id="52lndu"
sudo usermod -aG docker ubuntu
newgrp docker
```

## Restart Kubernetes

```bash id="5d8q4e"
sudo systemctl restart kubelet
```

## Check Cluster Nodes

```bash id="84g02j"
kubectl get nodes
```

---

# 📸 Project Screenshots

## Frontend UI

<img width="1013" height="630" alt="Image" src="https://github.com/user-attachments/assets/7a149bdf-14f0-4752-85bf-caa9437576da" />

## Kubernetes Pods

<img width="1003" height="379" alt="Image" src="https://github.com/user-attachments/assets/c305e918-ef0b-4fff-adfe-944fbd2b3d8c" />

## GitHub Actions Pipeline

In Process

---

# 🎯 Features

✅ Three-Tier Architecture
✅ Kubernetes Deployment
✅ Dockerized Application
✅ CI/CD Automation
✅ AWS Cloud Deployment
✅ Scalable Infrastructure
✅ DevOps Best Practices

---

# 👨‍💻 Author

**Damandeep Kaur**

GitHub: https://github.com/ImDamandeepKaur

---

# ⭐ Acknowledgements

Inspired by the `#TWSThreeTierAppChallenge` by TrainWithShubham Community.
