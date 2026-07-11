# GoodDeeds Kubernetes Homelab
## Phase 1 Complete

Date: 11 July 2026

---

## Objective

Deploy the GoodDeeds FastAPI application on Kubernetes using Minikube.

---

## Components Deployed

- Kubernetes Namespace
- ConfigMap
- Secret
- PostgreSQL Deployment
- PostgreSQL Service
- Persistent Volume Claim
- Redis Deployment
- Redis Service
- FastAPI Deployment
- NodePort Service

---

## Final Architecture

Client
   │
NodePort Service
   │
GoodDeeds API
   │
 ├── PostgreSQL
 └── Redis

---

## Kubernetes Concepts Learned

- Namespace
- Deployment
- ReplicaSet
- Pod
- Service
- ConfigMap
- Secret
- Persistent Volume Claim
- Environment Variables
- Rolling Update

---

## Major Issues Faced

### 1. Secret Missing

Error

```
CreateContainerConfigError
```

Cause

Deployment referenced a Secret that didn't exist.

Fix

```
kubectl apply -f secret.yaml
```

---

### 2. ConfigMap Missing

Error

```
CreateContainerConfigError
```

Fix

```
kubectl apply -f configmap.yaml
```

---

### 3. Redis Not Running

Cause

Redis deployment was never applied.

Fix

```
kubectl apply -f redis/
```

---

### 4. PostgreSQL PVC

Learned how Persistent Volume Claims are created and attached to Deployments.

---

### 5. ErrImageNeverPull

Error

```
ErrImageNeverPull
```

Cause

Deployment referenced

gooddeeds-api:v1

while Minikube contained

gooddeeds-api:v2

Fix

Updated

api/api-deployment.yaml

to

```
image: gooddeeds-api:v2
```

Loaded image

```
minikube image load gooddeeds-api:v2
```

Restarted deployment

```
kubectl rollout restart deployment gooddeeds-api -n gooddeeds
```

---

## Final Verification

Pods

✓ GoodDeeds API
✓ PostgreSQL
✓ Redis

Deployments

✓ Healthy

ReplicaSets

✓ Healthy

Logs

Application startup complete

Uvicorn running on port 8000

---

## Skills Learned

- Kubernetes YAML
- Deployments
- ReplicaSets
- Services
- ConfigMaps
- Secrets
- Persistent Storage
- Environment Variables
- Docker Images
- Image Loading
- Kubernetes Troubleshooting
- Rolling Updates
- Pod Lifecycle

---

## Resume Impact

This project demonstrates hands-on Kubernetes deployment and troubleshooting experience rather than tutorial-level knowledge.

---

## Next Phase

Phase 2

- Liveness Probe
- Readiness Probe
- Resource Limits