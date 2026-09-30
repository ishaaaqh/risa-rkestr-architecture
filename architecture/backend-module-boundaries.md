# BE-002-A — Backend Module Boundary Specification

**Project:** Rkestr — Work Orchestration Platform  
**Repository:** `risa-rkestr-architecture`  
**Ticket:** BE-002-A  
**Status:** Ready for implementation  
**Package root:** `com.risa.rkestr`

## 1. Objective

Define the backend business-module boundaries before implementation begins.

This specification establishes module ownership, dependency direction, cross-module communication, persistence ownership, public/internal boundaries, authorization boundaries, transaction boundaries, forbidden patterns, and the enforcement handoff to BE-002-B.

Rkestr is implemented initially as a **modular monolith**: one deployable Spring Boot application with explicit business-module boundaries and future extraction seams.

## 2. Architectural Principles

1. **Modular Monolith First** — one backend deployment initially; strong module boundaries.
2. **Business Capability Boundaries** — organize packages around capabilities, not global technical layers.
3. **Authoritative State** — PostgreSQL is the authoritative transactional datastore.
4. **Explicit Cross-Module Communication** — use stable contracts, ports, or events; never internal implementation access.
5. **Strong Consistency for Core Invariants** — authoritative business changes remain transactionally consistent.
6. **Transactional Outbox** — business state and outgoing event records are committed atomically.
7. **Server-Side Authorization** — workspace membership and permissions form the authorization boundary for workspace-owned resources.

## 3. Module Inventory

### Core domain modules

| Module | Responsibility |
|---|---|
| `identity` | User identity, credentials, authentication identities, sessions, account lifecycle |
| `workspace` | Workspace, membership, roles, permissions, invitations, workspace authorization |
| `workitem` | Work Item lifecycle, ownership, assignment, subtasks, dependencies, blockers |
| `classification` | Context, category, priority, importance, urgency, task nature, decision result |
| `deadline` | Planned start, soft/hard deadlines, temporal state and deadline evaluation |

### Supporting / derived modules

| Module | Responsibility |
|---|---|
| `reminder` | Reminder policies, plans, instances and scheduling |
| `notification` | Notification requests, templates, channel delivery and notification state |
| `event` | Outbox publication, event processing and consumer infrastructure |
| `search` | Search, filtering, sorting, saved views and read-model concerns |
| `audit` | Append-only audit records and audit infrastructure |

## 4. Module Ownership

### Identity
**Owns:** user identity, authentication credentials, authentication identities, sessions, password lifecycle, account lifecycle and authentication security events.

**Does not own:** workspace roles, workspace permissions, Work Item authorization or membership.

Identity answers: **Who is this user?**

### Workspace
**Owns:** workspace, workspace type, membership, roles, permissions, invitations, membership lifecycle and workspace authorization.

**Does not own:** credentials, authentication sessions or Work Item lifecycle.

Workspace answers: **What may this user do in this workspace?**

### Work Item
**Owns:** Work Item creation, lifecycle, Created By / Owner / Assignee, ownership transfer, subtasks, dependencies, blockers, deletion/restoration state and Work Item domain invariants.

**Does not own:** credentials, workspace permission definitions, reminder delivery, notification providers or search indexes.

Work Item is the authoritative owner of Work Item state.

### Classification
**Owns:** context, category, priority, importance, urgency, task nature, Eisenhower quadrant derivation and recommendation/explanation.

**Does not own:** lifecycle or notification/reminder delivery.

### Deadline
**Owns:** planned start, soft/hard deadlines and temporal evaluation: Upcoming, Due Soon, Due, Overdue and Delayed.

**Does not own:** lifecycle or notification/reminder delivery.

Deadline proximity may influence reminder planning or suggest urgency but must not silently change user-controlled classification.

### Reminder
**Owns:** reminder policy resolution, reminder plans, instances, lifecycle, deduplication, scheduling, cancellation, snooze, skip and expiry.

**Does not own:** notification provider implementation, Work Item lifecycle or authentication.

Reminder answers: **When should the user be reminded?**

### Notification
**Owns:** notification requests, templates, channel routing, delivery state and channel-specific delivery for in-app, push and email.

**Does not own:** why a reminder is required or Work Item business rules.

Notification answers: **How should a message be delivered?**

### Event
**Owns:** transactional outbox infrastructure, event publication, consumer processing, retries, dead letters and event-processing observability.

**Does not own:** business entities or authoritative business state.

### Search
**Owns:** search queries, filters, sorting, pagination, saved views and derived/read-model concerns.

**Does not own:** authoritative Work Item state, authorization rules, classification definitions or deadline rules.

PostgreSQL-backed search is the initial implementation; a dedicated search engine may be introduced only when justified.

### Audit
**Owns:** append-only audit records, audit persistence and audit retrieval.

Audit records capture relevant actor, action, resource, timestamp, workspace, old state, new state, correlation/request identifiers and reason where required.

Audit is not a replacement for application logs.

## 5. Dependency Rules

1. A module must not access another module's internal classes.
2. A module must not directly access another module's repository.
3. A module must not directly access another module's database tables.
4. Cross-module communication must use a stable contract, port or event.
5. There must be no circular module dependencies.
6. Infrastructure implementation details must not become business-module dependencies.
7. Domain logic must not depend on controllers, repositories, brokers, HTTP clients or framework-specific infrastructure.
8. Authorization must be enforced at the server-side application boundary.
9. Search must never become the source of truth for Work Item state.
10. Notification must not contain Work Item reminder/business-decision rules.

## 6. Dependency Matrix

| From | Allowed dependency / interaction |
|---|---|
| `identity` | `event`, `audit` |
| `workspace` | `identity`, `workitem`, `event`, `audit` |
| `workitem` | `workspace`, `classification`, `deadline`, `event`, `audit` |
| `classification` | `workitem`, `deadline`, `event`, `audit` |
| `deadline` | `workitem`, `event`, `audit` |
| `reminder` | `workspace`, `workitem`, `classification`, `deadline`, `notification`, `event`, `audit` |
| `notification` | `workspace`, `event`, `audit` |
| `event` | `reminder`, `notification`, `search`, `audit` |
| `search` | `workspace`, `workitem`, `classification`, `deadline` |
| `audit` | self / infrastructure only |

An allowed dependency never permits access to another module's internals.

For example, `workitem → workspace` means Work Item may invoke an explicit Workspace authorization contract. It does **not** mean direct access to `workspace.infrastructure.repository`.

## 7. Cross-Module Communication

### Synchronous module contracts

Use when the caller requires an immediate result for the current business operation.

Examples:

- Work Item → Workspace authorization
- Work Item → Classification validation
- Work Item → Deadline validation
- Search → Workspace authorization context

The receiving module exposes a stable application-level contract.

### Domain / integration events

Use when the receiving module does not need to participate in the same synchronous business transaction.

Examples include:

- `WorkItemCreated`
- `WorkItemUpdated`
- `WorkItemCompleted`
- `WorkItemCancelled`
- `WorkItemDeleted`
- `WorkItemRestored`
- `WorkItemOwnershipTransferred`
- `WorkItemClassificationChanged`
- `WorkItemDeadlineChanged`

Potential consumers include Reminder, Notification, Search, Audit and future analytics/integration consumers.

Events communicate facts that have already happened.

### Transactional Outbox

Authoritative state and outgoing event records are committed atomically:

```text
Request
  |
  v
Application Service
  |
  +----> Authoritative DB State
  |
  +----> Outbox Record
              |
              v
       Event Publisher
              |
              v
           Broker
              |
       +------+------+------+
       |      |      |      |
       v      v      v      v
   Reminder Search Audit Notification
```

## 8. Public and Internal Boundaries

Each module should use:

```text
<module>/
├── api/
├── application/
├── domain/
└── infrastructure/
```

### `api`
External-facing contracts such as REST controllers and request/response DTOs where appropriate.

### `application`
Use cases, application services, transaction orchestration and module-facing contracts.

### `domain`
Aggregates, entities/value objects, domain rules, domain services where required and domain events. Domain code remains independent of infrastructure.

### `infrastructure`
Persistence implementations, database mappings, broker adapters, external clients and framework-specific configuration.

Infrastructure implements technical concerns; it does not redefine business ownership.

## 9. Persistence Ownership

All modules initially use the same PostgreSQL database:

```text
rkestr
```

A shared database does **not** mean shared ownership.

Conceptually:

```text
identity       → identity-owned tables
workspace      → workspace-owned tables
workitem       → workitem-owned tables
classification → classification-owned tables
deadline       → deadline-owned tables
reminder       → reminder-owned tables
notification   → notification-owned tables
event          → outbox/event-processing tables
search         → search/read-model tables
audit          → audit-owned tables
```

Rules:

- A module may read/write its own tables.
- A module must not query another module's tables directly.
- Cross-module data comes through contracts or approved read models.
- Database foreign keys may be used within a module's owned persistence boundary.
- Cross-module relational coupling must not become a shortcut around application contracts.

## 10. Authorization Boundary

Workspace owns authorization.

Expected flow:

```text
HTTP Request
    |
    v
Identity
    |
    v
Workspace Authorization
    |
    v
Target Module Use Case
    |
    v
Domain Rules
```

For a Work Item operation:

```text
User
 |
 v
Work Item API
 |
 v
Work Item Application Service
 |
 +--> Workspace Authorization Contract
 |
 +--> Work Item Domain Rules
 |
 +--> Work Item Persistence
 |
 +--> Outbox
```

The backend must validate authentication, workspace membership, role/permission and operation-specific resource rules. Authorization must never be delegated to the frontend.

## 11. Transaction Boundaries

Transactions align with authoritative business state.

```text
Begin Transaction
    |
    +-- Validate command
    +-- Authorize operation
    +-- Load aggregate
    +-- Apply domain rules
    +-- Persist authoritative state
    +-- Persist audit record where required
    +-- Persist outbox event
Commit
```

After commit:

```text
Outbox
   |
   v
Event Publisher
   |
   v
Consumers
   |
   +--> Reminder
   +--> Notification
   +--> Search
   +--> Other derived processing
```

External calls should not be required for successful commitment of authoritative state unless explicitly justified.

## 12. Forbidden Patterns

### Global technical-layer packaging

Do not organize the application primarily as:

```text
controller/
service/
repository/
entity/
```

This hides business boundaries.

### Cross-module repository access

Forbidden:

```text
workitem → workspace.repository.WorkspaceRepository
```

Required:

```text
workitem → workspace authorization contract
```

### Cross-module entity reuse

A module must not use another module's persistence entity as its domain model.

### Shared "God" service

Do not create services such as:

```text
CommonBusinessService
PlatformService
TaskManagerService
EverythingService
```

Shared technical infrastructure is not a business-domain dumping ground.

### Business logic inside infrastructure

Repositories, controllers, broker adapters and external clients must not become owners of business rules.

### Event module owning domain state

The event module must not become authoritative owner of Work Items, users, workspaces or reminders.

### Search as source of truth

Search/read models must never determine authoritative Work Item state.

### Notification owning reminder decisions

Reminder determines when/why a reminder occurs. Notification determines how it is delivered.

### Circular dependencies

Avoid cycles such as:

```text
workitem → reminder → workitem
workspace → workitem → workspace
classification → workitem → classification
```

Use events/contracts or reconsider the boundary.

## 13. Package Convention

Package root:

```text
com.risa.rkestr
```

Business modules:

```text
com.risa.rkestr.identity
com.risa.rkestr.workspace
com.risa.rkestr.workitem
com.risa.rkestr.classification
com.risa.rkestr.deadline
com.risa.rkestr.reminder
com.risa.rkestr.notification
com.risa.rkestr.event
com.risa.rkestr.search
com.risa.rkestr.audit
```

When implementation artifacts are introduced:

```text
com.risa.rkestr.<module>.api
com.risa.rkestr.<module>.application
com.risa.rkestr.<module>.domain
com.risa.rkestr.<module>.infrastructure
```

The exact subpackage structure may evolve inside a module without changing the module boundary.

## 14. Architecture Enforcement — BE-002-B

BE-002-A defines the architecture.

BE-002-B will enforce it in `risa-rkestr-backend` by:

1. Adding ArchUnit.
2. Establishing module package rules.
3. Preventing forbidden cross-module dependencies.
4. Preventing direct access to another module's internal packages.
5. Preventing circular module dependencies.
6. Establishing automated architecture tests.
7. Making architecture violations fail CI.

Architecture tests are guardrails, not a substitute for engineering judgment.

## 15. Future Extraction Seams

The following are intentionally structured for possible future extraction if scale, ownership, deployment independence or operational requirements justify it:

- Reminder
- Notification
- Search
- Event processing
- Audit
- Potentially Identity / Workspace

The initial deployment remains a modular monolith. Service extraction is a response to demonstrated need, not an MVP requirement.

## 16. Relationship to Existing Architecture

This specification makes concrete the backend modularity principles established in:

- `ARCH-002` — Final Architecture Documentation
- `ARCH-003` — Architecture Diagrams
- `ARCH-004` — Definition of Done & Engineering Workflow

Relevant principles include modular monolith first, explicit business boundaries, strong consistency for authoritative state, transactional outbox, server-side authorization, asynchronous derived processing and future service extraction seams.

## 17. Definition of Done

- [x] All backend business modules are explicitly listed.
- [x] Each module has a documented responsibility boundary.
- [x] Core and supporting modules are identified.
- [x] Dependency relationships are documented.
- [x] Cross-module communication rules are documented.
- [x] Persistence ownership is documented.
- [x] Public/internal boundaries are documented.
- [x] Authorization ownership is documented.
- [x] Transaction boundaries are documented.
- [x] Forbidden architectural patterns are documented.
- [x] Initial package convention is documented.
- [x] BE-002-B enforcement scope is defined.
- [x] No new business capability is introduced beyond the frozen architecture.

## 18. Implementation Handoff

**BE-002-A**
- Deliverable: Architecture specification
- Repository: `risa-rkestr-architecture`
- Suggested commit:

```text
docs(architecture): define backend module boundaries
```

**BE-002-B**
- Deliverable: Automated architecture enforcement
- Repository: `risa-rkestr-backend`

Implementation sequence:

```text
Add ArchUnit
    ↓
Define module package rules
    ↓
Define allowed dependencies
    ↓
Define forbidden internal access
    ↓
Add architecture tests
    ↓
Run Maven tests
    ↓
Commit and push
```

BE-002-A should be committed before BE-002-B implementation begins.
