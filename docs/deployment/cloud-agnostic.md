# Cloud-Agnostic Deployment Strategy

Milky-Way uses a portability-first strategy: all services are shipped as OCI containers and deployed to Kubernetes with provider-neutral primitives. Provider-specific dependencies are isolated to overlays.

## Provider overlays
| Provider | Overlay Path | Purpose |
| --- | --- | --- |
| Azure | `infra/k8s/overlays/azure` | StorageClass, workload identity, ingress classes |
| GCP | `infra/k8s/overlays/gcp` | GKE-specific storage class and service annotations |
| Databricks | `infra/k8s/overlays/databricks` | Databricks workspace secrets and network policy stubs |

## Databricks integration
- Use the Databricks SQL Connector with Unity Catalog REST APIs.
- Configure service principals or OAuth tokens via secrets.
- Use VPC/VNet peering or Private Link for secure traffic.

## Model hosting options
- **Managed API** (OpenAI/Anthropic/Gemini): configure via `LLM_PROVIDER` and API keys.
- **Self-hosted** (vLLM): deploy as a GPU-backed service in the same cluster.

## Storage & databases
- PostgreSQL can be self-managed StatefulSet or a managed service (Cloud SQL, Azure Database for PostgreSQL).
- Vector store can be managed (Pinecone/Weaviate) or self-hosted.

## Network and security
- Enforce TLS termination at ingress.
- Use mTLS or service mesh for internal traffic if required.
- Enable audit logs in API gateway and metadata layer.
