# Kubernetes Deployment Guide

This guide describes a cloud-agnostic deployment model for Milky-Way using Kubernetes. Provider-specific tweaks live in overlays (see cloud-agnostic guide).

## Prerequisites
- Kubernetes 1.27+
- Ingress controller (Nginx or Istio)
- External secrets manager (Vault, GCP Secret Manager, Azure Key Vault)
- Container registry for service images

## Base deployment (provider-agnostic)
The base manifests in `infra/k8s/base` deploy the core services:
- `frontend`
- `api-gateway`
- `agent-engine`
- `worker-pool`
- `metadata-db`
- `cache`
- `vector-store`
- `observability`

Apply with Kustomize:
```bash
kubectl apply -k infra/k8s/base
```

## Autoscaling
- **HPA** is included for stateless services (frontend, api-gateway, agent-engine, worker-pool).
- **KEDA** can be added in overlays for queue depth scaling.

## Persistence
- `metadata-db` and `cache` are StatefulSets with PVCs.
- Define storage class in overlays to match your cloud provider.

## Secrets
- Secret refs are placeholders in base manifests.
- Bind secrets using external secret controllers in overlays.

## Observability
- Provide Prometheus and Grafana via helm or your existing stack.
- Enable tracing with OpenTelemetry collector if required.

## Deployment checklist
- [ ] Configure OAuth/OIDC with your SSO provider.
- [ ] Configure Databricks SQL Warehouse and Unity Catalog access.
- [ ] Load playbooks and ontologies into the metadata store.
- [ ] Validate agent graph endpoints with smoke tests.
