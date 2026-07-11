# Troubleshooting

## ErrImageNeverPull

Symptoms

Pod stuck in Pending

Diagnosis

kubectl describe pod

Root Cause

Deployment referenced image v1

Minikube contained image v2

Solution

Updated deployment image
Loaded image
Restarted deployment