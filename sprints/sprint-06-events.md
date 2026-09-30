# Sprint 6 — Notifications & Event Processing

## Frozen decisions

- Notification/Event Processing remains inside the Modular Monolith
- Broker and consumer boundaries provide future extraction seams
- Transactional Outbox
- At-least-once delivery
- Idempotent consumers
- Retry with exponential backoff + jitter
- DLQ
- Poison-message handling
- Business-key ordering
- Notification request abstraction
- In-App, Push, Email
- User notification preferences
- Workspace mandatory notification policies
- Deduplication
- Rate limiting / storm prevention
- Channel isolation
- Correlation + causation IDs
- Versioned event contracts

Notification provider failure must never roll back authoritative Work Item state.
