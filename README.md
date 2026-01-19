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
Open in browser:

http://localhost:8080/

Phase 2 — Configure AWS CLI & IAM
---------------------------------------------------------
1. Create AWS Account and IAM User

Create an IAM user with programmatic access and permissions for:

Amazon ECR

Amazon EKS

IAM (PassRole if required)

2. Configure AWS CLI
aws configure


Use:

Default region: eu-west-2

Output format: json

Verify authentication:

aws sts get-caller-identity

Phase 3 — Push Docker Image to AWS ECR
-----------------------------------------------------------------------
1. Create ECR Repository

AWS Console → ECR → Create repository

Example:

Repository name: whiteboard-aws

Repository URI:

434439813077.dkr.ecr.eu-west-2.amazonaws.com/whiteboard-aws

2. Authenticate Docker to ECR
aws ecr get-login-password --region eu-west-2 | docker login --username AWS --password-stdin 434439813077.dkr.ecr.eu-west-2.amazonaws.com

3. Build, Tag and Push Image
docker build -t whiteboard-aws .
docker tag whiteboard-aws:latest 434439813077.dkr.ecr.eu-west-2.amazonaws.com/whiteboard-aws:latest
docker push 434439813077.dkr.ecr.eu-west-2.amazonaws.com/whiteboard-aws:latest

Phase 4 — Create EKS Cluster
------------------------------------------------------------------------------------------

⚠️ Delete any previous EKS clusters or CloudFormation stacks before creating a new one.

Create the cluster:

eksctl create cluster \
  --name whiteboard-eks \
  --version 1.30 \
  --region eu-west-2 \
  --nodegroup-name whiteboard-nodes \
  --node-type t3.medium \
  --nodes 3 \
  --nodes-min 3 \
  --nodes-max 6 \
  --managed
Update kubeconfig:

aws eks update-kubeconfig --region eu-west-2 --name whiteboard-eks


Verify nodes:

kubectl get nodes

Phase 5 — Deploy Kubernetes Resources
------------------------------------------------------------
1. Navigate to Kubernetes YAML directory
cd C:\Users\jothy\OneDrive\Desktop\k8s

2. Update Image in Deployment

Edit whiteboard-deployment.yaml:

image: 434439813077.dkr.ecr.eu-west-2.amazonaws.com/whiteboard-aws:latest

3. Apply Kubernetes YAML Files

Deploy application:

kubectl apply -f whiteboard-deployment.yaml
kubectl apply -f whiteboard-service.yaml


Deploy Redis:

kubectl apply -f redis-deployment.yaml
kubectl apply -f redis-service.yaml


Check pods:

kubectl get pods -o wide


Check services and external IP:

kubectl get svc


Access the application:

http://<EXTERNAL-IP>:<PORT>/

Monitoring (Optional)

View resource usage:

kubectl top nodes
kubectl top pods

Troubleshooting
External IP shows <pending>

Wait a few minutes and recheck:

kubectl get svc


Ensure Service type is LoadBalancer

Pods stuck in ImagePullBackOff

Confirm ECR image URI is correct

Ensure image was pushed successfully

Inspect pod events:

kubectl describe pod <pod-name>

Kubernetes authentication issues
aws eks update-kubeconfig --region eu-west-2 --name whiteboard-eks
kubectl get nodes
Author

Jothy Shivani Sureshkumar

This project demonstrates hands-on experience with AWS, Docker, Kubernetes, EKS, ECR, and Redis, following real-world DevOps and cloud deployment practices.
