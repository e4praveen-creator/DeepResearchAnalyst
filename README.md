# DeepResearchAnalyst

Milky-Way is an enterprise analyst co-worker for deep research, hypothesis-driven analysis, and narrative reporting. This repository provides a technology-agnostic blueprint with container-first service boundaries, Kubernetes manifests, and deployment guidance for Azure, Databricks, and GCP.

## What is in this repo
- **Architecture blueprint** with the LangGraph agent graph, data platform, and business context layers.
- **Kubernetes base manifests** (provider-agnostic) for all core services.
- **Cloud overlays** for Azure, GCP, and Databricks-specific integrations.
- **Service contracts** outlining APIs, event streams, and configuration.

## Quick start (architecture only)
1. Review the architecture overview: [`docs/architecture/overview.md`](docs/architecture/overview.md)
2. Review the deployment guide: [`docs/deployment/kubernetes.md`](docs/deployment/kubernetes.md)
3. Review cloud-specific overlays: [`docs/deployment/cloud-agnostic.md`](docs/deployment/cloud-agnostic.md)

## Repository structure
```
docs/
  architecture/
  deployment/
infra/
  k8s/
    base/
    overlays/
services/
```

## Status
This is an architecture-first scaffolding intended to be deployed on any Kubernetes provider with autoscaling.
