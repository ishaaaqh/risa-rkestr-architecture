# Rkestr Architecture

**Product:** Rkestr  
**Positioning:** Enterprise Work Orchestration Platform  
**Tagline:** Work. Orchestrated.  
**Product ecosystem:** RISA

This repository is the architectural source of truth for Rkestr.

It documents:
- Product requirements and terminology
- Architecture decisions
- Backend and frontend architecture
- Domain and data models
- User and data flows
- API governance
- Security and enterprise NFRs
- Sprint plans and implementation decisions
- Deployment and production architecture

## Repository boundaries

| Repository | Responsibility |
|---|---|
| `risa-rkestr-architecture` | Why, what, and how the system is designed |
| `risa-rkestr-backend` | Spring Boot implementation, tests, local infrastructure, CI |
| `risa-rkestr-frontend` | Next.js/React implementation, tests, local infrastructure, CI |

Real secrets are never committed to any repository.

## Current architecture

Rkestr starts as a **Modular Monolith** with strong module boundaries and event-driven asynchronous processing.

Core infrastructure:
- Spring Boot backend
- Next.js/React frontend
- PostgreSQL as authoritative datastore
- Transactional Outbox
- Message Broker
- Object Storage for attachments
- Optional Redis
- Containerized deployment
- Kubernetes for application/workers when production requires it
- Managed infrastructure where practical

## Architectural status

Sprints 0–9 are architecturally defined and frozen.

Implementation starts with a new engineering Sprint 0 focused on repository and development foundations.
