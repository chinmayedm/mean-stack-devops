# MEAN Stack DevOps CI/CD Deployment

## 📌 Project Overview

This project demonstrates a complete CI/CD pipeline for a Dockerized MEAN stack application deployed on AWS EC2 using GitHub Actions and Docker Hub.

---

## 🛠️ Tech Stack

- MongoDB
- Express.js
- Angular
- Node.js
- Docker
- Docker Compose
- GitHub Actions
- AWS EC2
- Nginx

---

## 🐳 Docker Setup

### Backend Dockerfile
Located in: `backend/Dockerfile`

Builds Node.js backend service.

### Frontend Dockerfile
Located in: `frontend/Dockerfile`

Builds Angular production build and serves using Nginx.

---

## 🐳 Docker Compose

File: `docker-compose.yml`

Services:
- MongoDB
- Backend
- Frontend
- Nginx (if configured)

Run locally:

```bash
docker-compose up --build
```

---

## 🚀 CI/CD Pipeline

CI/CD is configured using GitHub Actions.

Workflow file:
```
.github/workflows/deploy.yml
```

Pipeline Steps:
1. Checkout code
2. Login to Docker Hub
3. Build Backend Image
4. Push Backend Image
5. Build Frontend Image
6. Push Frontend Image
7. SSH into EC2
8. Pull latest images
9. Restart containers

Trigger:
Push to `main` branch

---

## ☁️ AWS EC2 Deployment

Application deployed on:
- Ubuntu EC2 Instance
- Docker installed
- Docker Compose installed

Deployment flow:
Git Push → GitHub Actions → Docker Hub → EC2 → Containers Restart

Public URL:
```
http://<EC2-PUBLIC-IP>
```

---

## 🌐 Nginx Configuration

Nginx is used to serve Angular frontend and reverse proxy backend API.

Config file:
```
nginx/nginx.conf
```

---

## 📸 Screenshots

### 1️⃣ CI/CD Workflow Configuration
(Insert screenshot of GitHub Actions YAML file)

### 2️⃣ Successful CI/CD Execution
(Insert screenshot of GitHub Actions showing green build)

### 3️⃣ Docker Images on Docker Hub
(Insert screenshot showing pushed backend & frontend images)

### 4️⃣ EC2 Docker Containers Running
(Insert screenshot of `docker ps` on EC2)

### 5️⃣ Application Running in Browser
(Insert screenshot of working UI)

### 6️⃣ Nginx Configuration
(Insert screenshot of nginx.conf file)

---

## ✅ Conclusion

This project demonstrates a complete end-to-end DevOps workflow including containerization, CI/CD automation, and cloud deployment.
