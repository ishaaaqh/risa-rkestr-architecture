# Non-Functional Requirements

The following categories are mandatory architectural concerns. Exact numerical targets are finalized during production engineering.

## Security
- Strong authentication
- Workspace-scoped authorization
- Resource-level authorization
- Protection against BOLA/IDOR
- Rate limiting
- Secure token/session management
- Encryption in transit and at rest
- Secret externalization
- Security event auditing

## Reliability
- Transactional Outbox
- At-least-once event delivery
- Idempotent consumers
- Retry with backoff and jitter
- Dead Letter Queue
- Poison-message isolation
- Graceful shutdown

## Availability
- Horizontally scalable application instances
- Independently scalable workers
- Health checks
- Rolling deployments
- Failure isolation

## Performance
- Cursor pagination
- Indexed PostgreSQL queries
- Bounded result sizes
- Query timeouts
- Rate limiting
- Queue/consumer monitoring

## Scalability
- Modular boundaries
- Independently scalable workers
- Broker partitioning by business key
- Future OpenSearch extraction seam
- Future selective service extraction

## Observability
- Structured logs
- Metrics
- Distributed traces
- Correlation IDs
- Causation IDs
- Event IDs
- Consumer metrics
- DLQ monitoring

## Data durability
- Automated backups
- Point-in-time recovery
- Encrypted backups
- Restore testing

## Recovery
RPO and RTO targets will be established against business requirements before production deployment.

## Auditability
Important security, administrative, ownership, classification, lifecycle, and bulk operations must be auditable.

## Maintainability
- Clear module boundaries
- Versioned migrations
- Versioned event contracts
- API versioning
- ADR-driven architectural decisions
