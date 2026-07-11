# GoodDeeds Kubernetes Homelab

> A production-inspired Kubernetes homelab that deploys a FastAPI application with PostgreSQL and Redis using Minikube. This project focuses on learning Kubernetes through real-world deployment, troubleshooting, and operational practices rather than following a simple tutorial.

---

# Project Overview

The objective of this project is to build, deploy, troubleshoot, and operate a multi-container application on Kubernetes while following production-like practices.

The project demonstrates:

- Docker image creation
- Kubernetes Deployments
- Kubernetes Services
- ConfigMaps
- Secrets Management
- Persistent Volumes (PVC)
- Rolling Updates
- Scaling Applications
- Kubernetes Troubleshooting
- Production-style configuration management

Rather than only deploying an application, this homelab intentionally documents real issues encountered during implementation and the process used to diagnose and resolve them.

---

# Architecture

```text
                   User
                     │
                     │
             NodePort Service
                     │
                     ▼
            FastAPI Application
                     │
          ┌──────────┴──────────┐
          │                     │
          ▼                     ▼
     PostgreSQL             Redis Cache
          │
          ▼
 Persistent Volume Claim
```

---

# Technology Stack

| Technology | Purpose |
|------------|---------|
| Kubernetes | Container Orchestration |
| Minikube | Local Kubernetes Cluster |
| Docker | Containerization |
| FastAPI | Backend API |
| PostgreSQL | Relational Database |
| Redis | In-memory Cache |
| ConfigMaps | Application Configuration |
| Secrets | Secure Configuration |
| Persistent Volume Claims | Database Persistence |

---

# Development Environment

- Windows 10
- WSL2 (Ubuntu 24.04)
- Docker Desktop
- Minikube
- kubectl
- FastAPI
- PostgreSQL 15
- Redis 7

---

# Project Structure

```text
gooddeed-kubernetes/

├── api/
├── postgresql/
├── redis/
│
├── namespace.yaml
├── secret.yaml
├── configmap.yaml
│
├── README.md
├── CHANGELOG.md
├── TROUBLESHOOTING.md
├── ROADMAP.md
└── docs/
```

---

# Features Implemented

✅ Kubernetes Namespace

✅ Deployments

✅ ReplicaSets

✅ Services

✅ ConfigMaps

✅ Secrets

✅ Persistent Volume Claims

✅ PostgreSQL Deployment

✅ Redis Deployment

✅ FastAPI Deployment

✅ NodePort Service

✅ Rolling Updates

✅ Application Scaling

✅ Production Configuration

---

# Kubernetes Skills Demonstrated

- Docker Image Creation
- Kubernetes Deployments
- ReplicaSets
- Services
- ConfigMaps
- Secrets
- Persistent Storage
- Environment Variables
- Service Discovery
- Rolling Updates
- Scaling Applications
- Kubernetes Debugging
- Pod Lifecycle Management
- Production Configuration Management

---

# Deployment

Clone the repository

```bash
git clone https://github.com/zaheerbeg21/gooddeed-kubernetes.git
```

Start Minikube

```bash
minikube start --driver=docker
```

Deploy all Kubernetes resources

```bash
kubectl apply -f namespace.yaml

kubectl apply -f secret.yaml

kubectl apply -f configmap.yaml

kubectl apply -f postgresql/

kubectl apply -f redis/

kubectl apply -f api/
```

Verify deployment

```bash
kubectl get all -n gooddeeds
```

---

# Troubleshooting Experience

During development, several production-like issues were intentionally investigated and resolved, including:

- Minikube driver configuration
- Missing Kubernetes Secrets
- Missing ConfigMaps
- CrashLoopBackOff
- ErrImageNeverPull
- Redis service discovery
- Application startup validation
- Rolling Update verification
- Image version mismatches
- Deployment recovery

Complete troubleshooting documentation is available in:

```
TROUBLESHOOTING.md
```

---

# Documentation

| File | Description |
|------|-------------|
| README.md | Project Overview |
| CHANGELOG.md | Progress History |
| TROUBLESHOOTING.md | Production Issues & Resolutions |
| ROADMAP.md | Upcoming Enhancements |
| docs/PHASE-01.md | Phase 1 Documentation |
| docs/PHASE-02.md | Health Checks (Upcoming) |

---

# Roadmap

## Phase 1 ✅

- Kubernetes Deployment
- PostgreSQL
- Redis
- ConfigMaps
- Secrets
- PVC
- Scaling
- Rolling Updates
- Troubleshooting

## Phase 2 (In Progress)

- Liveness Probe
- Readiness Probe
- Startup Probe
- Resource Requests
- Resource Limits

## Phase 3

- Ingress Controller
- Custom Domain
- TLS

## Phase 4

- Helm Charts

## Phase 5

- GitHub Actions CI/CD

## Phase 6

- Prometheus
- Grafana

## Phase 7

- Horizontal Pod Autoscaler

## Phase 8

- Deploy to AWS EKS

---

# Lessons Learned

- Secrets should never be hardcoded.
- ConfigMaps should manage application configuration.
- Always investigate logs before modifying deployments.
- Rolling updates minimize deployment downtime.
- Kubernetes Services provide stable service discovery.
- Production issues are best solved through systematic troubleshooting rather than trial and error.

---

# Resume Highlights

This project demonstrates practical experience with:

- Kubernetes Administration
- Docker
- Production-style Deployments
- FastAPI Containerization
- PostgreSQL & Redis on Kubernetes
- Persistent Storage
- Rolling Updates
- Scaling
- Kubernetes Troubleshooting
- DevOps Operational Practices

---

# License

This project is intended for educational and portfolio purposes.