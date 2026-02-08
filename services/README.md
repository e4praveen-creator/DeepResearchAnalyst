# Service Contracts (High-Level)

This file defines service boundaries so implementation can be swapped across clouds or tech stacks.

## frontend
- **Responsibilities**: Chat UI, dashboards, storyboards, SQL editor, schema browser.
- **Dependencies**: `api-gateway` for auth/session and API calls.
- **Protocols**: HTTPS + WebSocket.

## api-gateway
- **Responsibilities**: Auth, RBAC, routing, rate limiting, session management.
- **Dependencies**: Redis, metadata DB, agent engine.
- **Protocols**: HTTPS + WebSocket proxy.

## agent-engine
- **Responsibilities**: LangGraph orchestration, memory, tool routing.
- **Dependencies**: Metadata DB, vector store, Redis.
- **Protocols**: gRPC or HTTPS.

## worker-pool
- **Responsibilities**: SQL execution, EDA jobs, hypothesis validation.
- **Dependencies**: Databricks SQL Warehouse, Redis job queue.
- **Protocols**: gRPC or HTTPS.

## metadata-db
- **Responsibilities**: Users, playbooks, ontology metadata, feedback.
- **Storage**: PostgreSQL.

## cache
- **Responsibilities**: Session state, rate limiting, query cache.
- **Storage**: Redis.

## vector-store
- **Responsibilities**: Semantic search for ontology, playbooks, memory.
- **Storage**: Managed or self-hosted vector DB.
