# Milky-Way Architecture Overview

Milky-Way is a multi-agent, hypothesis-driven analyst co-worker designed to run across cloud providers. The system is built around three layers:

1. **Foundational Agent Layer**: LangGraph-orchestrated agents with a shared state machine that routes between Clarification, Hypothesis Generation, Data Mapping, Text-to-SQL, EDA, Visualization, and Reporting agents.
2. **Business Context Layer**: Playbooks, ontologies, hypothesis banks, and ground truths used to specialize the system for each domain.
3. **Composable Platform Layer**: Containerized services deployed on Kubernetes with autoscaling, observability, and model routing.

## Core services
| Service | Responsibility | Scaling Strategy |
| --- | --- | --- |
| `frontend` | React SPA, chat UI, dashboards, and storyboards | HPA on CPU/RPS |
| `api-gateway` | Auth, RBAC, routing, session management | HPA on CPU/RPS |
| `agent-engine` | LangGraph orchestration and memory | HPA on queue depth or CPU |
| `worker-pool` | SQL execution, EDA jobs | HPA/KEDA on job backlog |
| `metadata-db` | Postgres for user profiles, playbooks, and metadata | StatefulSet + PVC |
| `cache` | Redis for sessions and caching | StatefulSet + PVC |
| `vector-store` | Semantic retrieval for ontology, playbooks, memory | StatefulSet or managed |
| `observability` | Metrics, logs, tracing | DaemonSet + Deployment |

## Agent graph (Phase 1)
- **Orchestrator Agent** routes flow, manages state, and handles interrupts.
- **Clarification Agent** extracts intent, identifies ambiguity, and requests missing details.
- **Hypothesis Generation Agent** produces ranked hypotheses from playbooks and domain context.
- **Data Mapping Agent** maps hypotheses to schema fields and reports gaps.
- **Text-to-SQL Agent** generates Databricks SQL with validation and cost guardrails.
- **EDA Agent** executes statistical tests and feature analyses.
- **Visualization Agent** returns chart specs and dashboard layouts.
- **Insight Agent** synthesizes narrative summaries and recommendations.
- **Follow-Up Agent** suggests next-best questions and drill paths.

## Data flow (high level)
1. User logs in → persona and memory loaded.
2. Request enters the API gateway → Orchestrator Agent picks a path.
3. Agents run in a graph → SQL/EDA jobs executed by worker pool.
4. Results rendered with charts + narrative → feedback logged.
5. Memory updated → playbooks and ontologies enriched.

## Non-functional requirements
- **Performance**: <5s for descriptive queries, <3 minutes for deep diagnostics.
- **Security**: SSO (SAML/OIDC), RBAC, PII redaction, audit trails.
- **Reliability**: 99.9% uptime, durable storage, zero data loss.

## Technology-agnostic principles
- Container-first architecture with OCI images.
- Kubernetes-native primitives (Deployment, StatefulSet, HPA, Ingress).
- Provider-specific features isolated in overlays.
- Clear separation of control plane (agent orchestration) and data plane (SQL/EDA execution).
