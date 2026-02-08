# GCP Overlay

Use this overlay to customize storage classes, Workload Identity, and Ingress for GKE.

Suggested customizations:
- Set `storageClassName: premium-rwo` for PVCs.
- Add Google Workload Identity annotations to service accounts.
- Configure an ingress class for GKE Ingress or Nginx.
