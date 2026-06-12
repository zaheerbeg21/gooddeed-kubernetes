# GoodDeeds Kubernetes Homelab

## Project Overview

This project demonstrates deploying a containerized FastAPI application with PostgreSQL and Redis on Kubernetes using Minikube.

The objective was to gain hands-on experience with:

* Docker
* Kubernetes
* Minikube
* Deployments
* Services
* ConfigMaps
* Secrets
* Persistent Volumes
* Scaling
* Rolling Updates
* Troubleshooting CrashLoopBackOff issues


# Architecture

```text
                User
                  |
                  |
            NodePort Service
                  |
                  |
          GoodDeeds FastAPI
                  |
        --------------------
        |                  |
        |                  |
 PostgreSQL          Redis Cache
```

Components:

| Component             | Purpose                     |
| --------------------- | --------------------------- |
| FastAPI               | Backend API                 |
| PostgreSQL            | Database                    |
| Redis                 | Cache / Session Store       |
| Kubernetes Deployment | Pod Management              |
| Kubernetes Service    | Internal Communication      |
| Secret                | Sensitive Values            |
| ConfigMap             | Application Configuration   |
| PVC                   | Persistent Database Storage |


# Environment

* Windows 10
* WSL2 Ubuntu
* Docker Desktop
* Minikube
* Kubernetes
* FastAPI
* PostgreSQL 15
* Redis 7


# Project Structure

```text
gooddeed-kubernetes/

├── namespace.yaml
├── secret.yaml
├── configmap.yaml

├── api/
│   ├── api-deployment.yaml
│   └── api-service.yaml

├── postgresql/
│   ├── postgres-deployment.yaml
│   ├── postgres-service.yaml
│   └── postgres-pvc.yaml

└── redis/
    ├── redis-deployment.yaml
    └── redis-service.yaml
```


# Deployment Steps

## Start Minikube

```bash
minikube start --driver=docker
```

Verify:

```bash
kubectl get nodes
```


## Create Namespace

```bash
kubectl apply -f namespace.yaml
```


## Create Secret

```bash
kubectl apply -f secret.yaml
```


## Create ConfigMap

```bash
kubectl apply -f configmap.yaml
```


## Deploy PostgreSQL

```bash
kubectl apply -f postgresql/
```


## Deploy Redis

```bash
kubectl apply -f redis/
```


## Build API Docker Image

```bash
docker build -t gooddeeds-api:v1 .
```

Load image into Minikube:

```bash
minikube image load gooddeeds-api:v1
```


## Deploy API

```bash
kubectl apply -f api/
```


# Major Issues Faced and Resolution

## Issue 1: Minikube Driver Error

Error:

```text
DRV_UNSUPPORTED_OS:
The driver '' is not supported on linux/amd64
```

Cause:

Minikube profile was corrupted and driver was not configured.

Resolution:

```bash
minikube delete
minikube start --driver=docker
```


## Issue 2: Redis Service Missing

Problem:

Redis deployment was running but no service existed.

Verification:

```bash
kubectl get svc -n gooddeeds
```

Only PostgreSQL service was visible.

Cause:

redis-service.yaml was empty.

Resolution:

Created Redis service manifest and applied:

```bash
kubectl apply -f redis-service.yaml
```

Result:

```text
redis-service created
```


## Issue 3: API Pod CrashLoopBackOff

Error:

```text
CrashLoopBackOff
```

Investigation:

```bash
kubectl logs deployment/gooddeeds-api -n gooddeeds
```

Found:

```text
ValidationError:
Insecure default values in production
```


## Issue 4: Missing SECRET_KEY

Error:

```text
Insecure default values in production:
secret_key
```

Cause:

Application required SECRET_KEY environment variable.

Fix:

Added:

```yaml
SECRET_KEY: super-secret-key-for-kubernetes
```

to Kubernetes Secret.

Applied:

```bash
kubectl apply -f secret.yaml
```

Restarted deployment:

```bash
kubectl rollout restart deployment gooddeeds-api -n gooddeeds
```


## Issue 5: Missing FIRST_ADMIN_PASSWORD

Error:

```text
Insecure default values in production:
first_admin_password
```

Cause:

Application startup validation required admin password.

Fix:

Added:

```yaml
FIRST_ADMIN_PASSWORD: admin123
```

to secret.yaml.

Applied:

```bash
kubectl apply -f secret.yaml

kubectl rollout restart deployment gooddeeds-api -n gooddeeds
```

Result:

```text
Pod Status: Running
```


# Kubernetes Troubleshooting Commands Used

View Pods:

```bash
kubectl get pods -n gooddeeds
```

Describe Pod:

```bash
kubectl describe pod <pod-name> -n gooddeeds
```

View Logs:

```bash
kubectl logs deployment/gooddeeds-api -n gooddeeds
```

View Events:

```bash
kubectl get events -n gooddeeds --sort-by=.metadata.creationTimestamp
```

Check Services:

```bash
kubectl get svc -n gooddeeds
```

Check Deployments:

```bash
kubectl get deployment -n gooddeeds
```


# Scaling Test

Scaled API replicas:

```bash
kubectl scale deployment gooddeeds-api --replicas=3 -n gooddeeds
```

Result:

```text
3 Pods Running
```

Verified:

```bash
kubectl get deployment gooddeeds-api -n gooddeeds
```

Output:

```text
READY 3/3
```


# Rolling Update Test

Built new image:

```bash
docker build -t gooddeeds-api:v2 .
```

Loaded image:

```bash
minikube image load gooddeeds-api:v2
```

Updated deployment:

```bash
kubectl set image deployment/gooddeeds-api \
gooddeeds-api=gooddeeds-api:v2 \
-n gooddeeds
```

Verified:

```bash
kubectl rollout status deployment/gooddeeds-api -n gooddeeds
```

Result:

```text
deployment successfully rolled out
```


# Skills Demonstrated

* Docker Image Creation
* Kubernetes Deployments
* Kubernetes Services
* ConfigMaps
* Secrets Management
* Persistent Volumes
* Service Discovery
* FastAPI Deployment
* PostgreSQL Deployment
* Redis Deployment
* CrashLoopBackOff Troubleshooting
* Rolling Updates
* Scaling Applications
* Kubernetes Debugging
* Production Configuration Management


# Lessons Learned

* Never hardcode secrets inside containers.
* Use ConfigMaps for configuration.
* Use Secrets for sensitive data.
* Always inspect logs before modifying deployments.
* Kubernetes Services provide stable networking.
* Rolling updates prevent downtime.
* Minikube is excellent for learning production Kubernetes concepts.


# Future Improvements

* Add Ingress Controller
* Add TLS/HTTPS
* Add Horizontal Pod Autoscaler
* Add Prometheus Monitoring
* Add Grafana Dashboards
* Add CI/CD using GitHub Actions
* Deploy to AWS EKS
* Implement Helm Charts
* Add ArgoCD GitOps

```
```

