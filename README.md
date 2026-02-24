# 🚀 Production-Ready MEAN Stack CI/CD Deployment

## 📌 Project Overview

This project demonstrates a complete end-to-end DevOps implementation for deploying a Dockerized MEAN stack application to AWS EC2 using GitHub Actions as the CI/CD engine.

The objective of this project is to:

- Containerize a full-stack application
- Automate build and image publishing
- Implement secure SSH-based deployment
- Deploy containers on AWS EC2
- Serve production frontend using Nginx
- Maintain infrastructure and deployment best practices

This setup simulates a real-world production CI/CD workflow.

---

# 🏗️ Architecture Overview

### Deployment Flow

![CI/CD Architecture](https://github.com/chinmayedm/mean-stack-devops/blob/main/ci:cd.png?raw=true)

---

# 🛠️ Technology Stack

| Layer | Technology |
|--------|------------|
| Frontend | Angular |
| Backend | Node.js + Express |
| Database | MongoDB |
| Containerization | Docker |
| Orchestration | Docker Compose |
| CI/CD | GitHub Actions |
| Registry | Docker Hub |
| Cloud Provider | AWS EC2 |
| Web Server | Nginx |
| OS | Ubuntu Server |

---

# 🐳 Containerization

## 1️⃣ Backend Dockerfile

Location:
```
backend/Dockerfile
```

Purpose:
- Uses Node base image
- Installs dependencies
- Exposes API port
- Runs production server

Design Decision:
- Keeps image minimal
- Avoids unnecessary layers
- Production-ready configuration

---

## 2️⃣ Frontend Dockerfile

Location:
```
frontend/Dockerfile
```

Purpose:
- Multi-stage build
- Angular production build
- Served via lightweight Nginx image

Why Multi-Stage?
- Smaller final image
- No dev dependencies in production
- Optimized static delivery

---

## 3️⃣ Docker Compose Configuration

File:
```
docker-compose.yml
```

Services:

- MongoDB (Persistent volume)
- Backend API
- Angular Frontend (Nginx)
- Internal Docker networking

Key Features:
- Service dependency management
- Restart policy
- Port mapping
- Volume persistence

---

# 🔄 CI/CD Pipeline

Workflow File:
```
.github/workflows/deploy.yml
```

Trigger:
Push to `main` branch

---

## Pipeline Stages

### ✅ 1. Checkout Code
Fetch latest source.

### ✅ 2. Docker Authentication
Secure login using GitHub Secrets.

### ✅ 3. Build Backend Image
Tagged as:
```
<docker-username>/mean-backend:latest
```

### ✅ 4. Push Backend Image
Stored in Docker Hub.

### ✅ 5. Build Frontend Image
Production optimized.

### ✅ 6. Push Frontend Image
Stored in Docker Hub.

### ✅ 7. SSH Deployment
Secure SSH using:
- Private key stored in GitHub Secrets
- No password authentication

### ✅ 8. Remote Deployment Commands
On EC2:
```
docker-compose pull
docker-compose down
docker-compose up -d
```

Zero manual intervention required.

---

# ☁️ AWS Infrastructure

## EC2 Configuration

- Ubuntu 22.04
- t2.micro (or similar)
- Public IP assigned
- Security Group:
  - Port 22 (SSH)
  - Port 80 (HTTP)

---

## Docker Installation

Installed:
- Docker Engine
- Docker Compose

---

## Nginx Setup

Frontend container uses Nginx to:

- Serve Angular production build
- Handle static files efficiently
- Reverse proxy API calls (if configured)

Why Nginx?

- High performance
- Production-grade
- Lightweight
- Industry standard

---

# 🔐 Security Considerations

- Secrets stored in GitHub Actions Secrets
- No hardcoded credentials
- SSH key authentication
- Docker images built in isolated runner
- No direct EC2 manual deployment

---

# 🚀 Step-by-Step Setup Guide

## Step 1: Clone Repository

```
git clone https://github.com/<your-username>/mean-stack-devops.git
cd mean-stack-devops
```

---

## Step 2: Configure Docker Hub Secrets

In GitHub → Settings → Secrets → Actions:

Add:

- DOCKER_USERNAME
- DOCKER_PASSWORD
- EC2_HOST
- EC2_USERNAME
- EC2_SSH_KEY
- EC2_PORT

---

## Step 3: Setup EC2

On EC2:

```
sudo apt update
sudo apt install docker.io docker-compose -y
sudo systemctl start docker
```

Clone repo:

```
git clone https://github.com/<your-username>/mean-stack-devops.git
```

---

## Step 4: Trigger CI/CD

Push to main:

```
git push origin main
```

GitHub Actions will automatically:

- Build images
- Push to Docker Hub
- Deploy to EC2

---

# 🌍 Application Access

Open:

```
http://<EC2-PUBLIC-IP>
```

Application runs live in production container environment.

---

# 📸 Screenshots

## 1️⃣ CI/CD Configuration
Screenshot of:
```
.github/workflows/deploy.yml
```

---

## 2️⃣ Successful CI/CD Execution
![ci/cd](https://github.com/chinmayedm/mean-stack-devops/blob/main/Screenshot%202026-02-24%20at%2000.36.01.png?raw=true)

---

## 3️⃣ Docker Image Build & Push
![Backend-Frontend](https://github.com/chinmayedm/mean-stack-devops/blob/main/Screenshot%202026-02-24%20at%2000.41.45.png?raw=true)

---

## 4️⃣ EC2 Container Deployment
Screenshot of:
```
docker ps
```

---

## 5️⃣ Working Application UI
Screenshot of:
Browser displaying live application

---

## 6️⃣ Nginx Configuration
Screenshot of:
```
frontend/Dockerfile
```
and/or
```
nginx/nginx.conf
```

---

# 📊 Infrastructure Summary

| Component | Role |
|------------|------|
| GitHub | Source Control |
| GitHub Actions | CI/CD Engine |
| Docker Hub | Image Registry |
| AWS EC2 | Compute Instance |
| Docker | Container Runtime |
| Docker Compose | Service Orchestration |
| Nginx | Web Server |
| MongoDB | Database |

---

# ✅ Conclusion

This project demonstrates a production-style DevOps implementation including:

- Full containerization
- Automated CI/CD
- Secure secret handling
- Cloud deployment
- Service orchestration
- Zero-downtime deployment model

The architecture is scalable and can be extended to:

- Kubernetes
- Terraform-based infrastructure
- Load balancing
- Auto-scaling groups
- SSL using Let's Encrypt

---

# 📌 Author

DevOps CI/CD Implementation  
MEAN Stack Production Deployment
This project demonstrates a complete end-to-end DevOps workflow including containerization, CI/CD automation, and cloud deployment.
