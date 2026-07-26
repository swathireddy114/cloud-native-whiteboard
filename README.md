# Cloud-Native Whiteboard Application

A cloud-native collaborative whiteboard application deployed on **Amazon Elastic Kubernetes Service (EKS)** using **Docker**, **Kubernetes**, **Amazon Elastic Container Registry (ECR)**, and **Redis**. The project demonstrates containerisation, orchestration, cloud deployment, and real-time data synchronisation in a scalable Kubernetes environment.

---

## Project Overview

This project focuses on deploying a collaborative whiteboard application using modern cloud-native technologies. The application is containerised with Docker, hosted on an Amazon EKS cluster, and uses Redis to maintain shared application state across multiple users.

The repository includes Kubernetes deployment and service configurations required to deploy both the application and Redis within a Kubernetes cluster.

---

## Key Features

- Real-time collaborative whiteboard application
- Docker containerisation
- Kubernetes-based deployment and orchestration
- Amazon EKS cluster deployment
- Amazon ECR container image management
- Redis integration for shared application state
- LoadBalancer service for external application access

---

## Architecture

```
Users
   │
   ▼
AWS Load Balancer
   │
   ▼
Kubernetes Service
   │
   ▼
Whiteboard Application Pods
   │
   ▼
Redis Service
   │
   ▼
Redis Pod
```

---

## Technology Stack

| Category | Technologies |
|----------|--------------|
| Programming | Node.js |
| Containerisation | Docker |
| Container Registry | Amazon ECR |
| Orchestration | Kubernetes |
| Cloud Platform | Amazon EKS |
| Database / Cache | Redis |
| Infrastructure Tools | AWS CLI, kubectl, eksctl |

---

## Repository Structure

```
.
├── README.md
├── redis.yaml
├── whiteboard-deployment.yaml
└── whiteboard-service.yaml
```

---

## Deployment Workflow

The deployment follows a cloud-native workflow:

1. Build the Docker image for the whiteboard application.
2. Push the image to Amazon Elastic Container Registry (ECR).
3. Create and configure an Amazon EKS cluster.
4. Deploy Redis using Kubernetes.
5. Deploy the whiteboard application using Kubernetes Deployment and Service resources.
6. Access the application through the Kubernetes LoadBalancer.

---

## Getting Started

### Prerequisites

- Docker Desktop
- Node.js (v18 or later)
- AWS CLI
- kubectl
- eksctl
- AWS Account with EKS and ECR permissions

### Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/cloud-native-whiteboard.git
cd cloud-native-whiteboard
```

### Deploy the Application

Create your EKS cluster and configure kubectl.

Deploy Redis:

```bash
kubectl apply -f redis.yaml
```

Deploy the application:

```bash
kubectl apply -f whiteboard-deployment.yaml
kubectl apply -f whiteboard-service.yaml
```

Verify deployment:

```bash
kubectl get pods
kubectl get svc
```

Access the application using the external IP assigned to the LoadBalancer service.

---

## Learning Outcomes

This project provided practical experience in:

- Cloud-native application deployment
- Docker containerisation
- Kubernetes deployments and services
- Amazon EKS cluster management
- Amazon ECR image management
- Redis integration within Kubernetes
- Cloud infrastructure and DevOps practices

---

## Future Enhancements

- Implement CI/CD using GitHub Actions
- Add HTTPS using AWS Application Load Balancer
- Integrate monitoring with Prometheus and Grafana
- Implement Horizontal Pod Autoscaling
- Add persistent storage for application data

---


