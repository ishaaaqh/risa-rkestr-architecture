# Deployment Architecture

## Production direction

```text
Internet
 |
Load Balancer / API Gateway
 |
Application Cluster
 |
 +-- PostgreSQL
 +-- Redis (optional)
 +-- Message Broker
 +-- Object Storage
 |
Workers
 +-- Reminder
 +-- Notification
 +-- Event processing
```

Observability spans all components.

## Kubernetes

Kubernetes is appropriate for:
- Application instances
- Workers
- Event consumers
- Scheduled workloads

Managed infrastructure is preferred where practical for:
- PostgreSQL
- Message Broker
- Object Storage
- Container Registry

## Environments

```text
Local
Development
Test / Integration
Staging / Preprod
Production
```

Initially implementation focuses on Local + Development.

## CI/CD

```text
Pull Request
 |
Compile / Build
 |
Unit Tests
 |
Integration Tests
 |
Static Analysis
 |
Security Scanning
 |
Container Build
 |
Development
 |
Staging
 |
Production
```

## Deployment

Rolling deployment initially.

Requirements:
- Readiness checks
- Liveness checks
- Graceful shutdown
- Connection draining
- Backward-compatible migrations

## Database migration

Use expand → migrate → contract for schema changes.

## Secrets

Real secrets must not be committed.

Use environment variables locally and managed secret storage for deployed environments.
