# Azure Overlay

Use this overlay to customize storage classes, workload identity, and ingress annotations for AKS.

Suggested customizations:
- Add `storageClassName` to StatefulSet PVCs (e.g., `managed-premium`).
- Add Azure Workload Identity annotations to service accounts.
- Configure an ingress class for Nginx or AGIC.
