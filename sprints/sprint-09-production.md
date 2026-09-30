# Sprint 9 — Production Engineering & Deployment

## Frozen decisions

- Modular Monolith remains the application deployment model
- Workers are independently scalable runtimes
- Kubernetes for application/workers where justified
- Managed PostgreSQL, broker, object storage, and registry where practical
- Infrastructure as Code
- Automated CI/CD
- Rolling deployments initially
- Liveness and readiness probes
- Graceful shutdown
- Independent API/worker scaling
- Redis optional, not authoritative
- Broker ordering by business key
- Logs + metrics + traces
- Security scanning in CI/CD
- Managed secret storage
- Backup and restore operations
- Expand → migrate → contract database migrations
