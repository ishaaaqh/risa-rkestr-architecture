# System Architecture Overview

## Architectural style

Rkestr uses a **Modular Monolith first** strategy.

We intentionally avoid premature microservices while creating strong internal boundaries and asynchronous extraction seams.

### Principle

> Commands change the world; events tell the rest of the system the world changed.

## Logical architecture

```text
Clients
  |
Load Balancer / API Gateway
  |
Rkestr Modular Monolith
  |
  +-- Identity
  +-- Workspace / RBAC
  +-- Work Item
  +-- Classification / Decision Engine
  +-- Deadline
  +-- Reminder
  +-- Notification
  +-- Search / Productivity
  +-- Audit
  +-- Shared / Infrastructure
  |
  +-- PostgreSQL
  |
  +-- Transactional Outbox
          |
      Event Publisher
          |
      Message Broker
       /    |     \
 Reminder Notification Analytics
 Worker     Worker    Worker
```

## Consistency

Strong consistency:
- Authoritative Work Item state
- Workspace membership
- Authorization invariants
- Ownership/assignment invariants
- Deadline state
- Subtasks/dependencies

Eventual consistency:
- Notifications
- Search/derived views where introduced
- Analytics
- Integrations
- Metrics

## Future evolution

If actual scale, ownership, deployment, or reliability requirements justify extraction, modules can become services without redesigning the domain model.
