# Whiteboard Application on AWS EKS + Redis

This project deploys a **real-time collaborative whiteboard application** on **AWS EKS (Kubernetes)** using **Docker**, **AWS ECR**, and **Redis** for shared state and caching.

The repository contains Kubernetes **Deployment** and **Service** YAML files for both the whiteboard application and Redis, demonstrating a real-world cloud-native deployment workflow.

---

## Architecture Overview
- Dockerised Node.js whiteboard application
- Container image stored in AWS ECR
- Kubernetes cluster hosted on AWS EKS
- Redis deployed as a Kubernetes service
- Application exposed using a LoadBalancer service

---

## Tech Stack
- Node.js (v18+ recommended)
- Docker & Docker Desktop
- AWS ECR (Elastic Container Registry)
- AWS EKS (Elastic Kubernetes Service)
- Kubernetes (kubectl)
- eksctl
- Redis

---

## Prerequisites

Ensure the following tools are installed and working:

- **Git** – clone repositories
- **Docker Desktop** – build and test containers
- **Node.js v18+** – optional local development
- **AWS CLI** – AWS authentication and services
- **kubectl** – Kubernetes CLI
- **eksctl** – EKS cluster creation and management

Verify installations:
```bash
git --version
docker --version
node -v
aws --version
kubectl version --client
eksctl version

Phase 1 — Run Application Locally
----------------------------------
Start Docker Desktop

Clone the whiteboard source code:

git clone https://github.com/cracker0dks/whiteboard.git
cd whiteboard
npm install
npm run start:dev

Run using Docker if a Dockerfile is present:

docker build -t whiteboard-aws .
docker run -d -p 8080:8080 whiteboard-aws
kubectl version --client
eksctl version
