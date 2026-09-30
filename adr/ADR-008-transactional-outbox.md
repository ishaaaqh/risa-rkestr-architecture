# ADR-008 — Transactional Outbox

## Status
Accepted

Authoritative state and outbox event are persisted in the same transaction.

A publisher asynchronously transfers events to the broker.

Consumers assume at-least-once delivery and are idempotent.
