# Kubernetes Web Application Deployment

This repository contains a YAML manifest for deploying a web application in Kubernetes, considering the following requirements:

- Application initialization time: 5–10 seconds
- CPU burst at startup, then stable around 0.1 CPU
- Stable memory usage around 128Mi
- Multi-zone cluster with 3 zones and 5 nodes
- Peak load requires 4 replicas
- Daily load pattern: high during the day, low at night
- Goals: maximum availability and minimal resource usage

## What’s inside

- **Deployment** with 4 replicas configured for startup characteristics
- **Horizontal Pod Autoscaler (HPA)** scaling from 1 to 5 replicas based on CPU usage
- **PodDisruptionBudget (PDB)** ensuring at least 3 replicas are always available
- **Pod Anti-Affinity** to distribute pods evenly across zones

## Why this setup

- CPU request set to 300m to cover startup CPU bursts
- Memory request fixed at 128Mi based on stable usage
- HPA scales down to 1 replica at night to save resources
- Anti-affinity prevents pods from scheduling in the same zone, enhancing resilience
- `startupProbe` prevents premature restarts during long application startup
- Readiness and liveness probes ensure stability during startup and normal operation

## How to apply

```bash
kubectl apply -f .
