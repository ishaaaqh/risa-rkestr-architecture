# Data Architecture

PostgreSQL is the authoritative system of record.

## Conceptual model

```text
User
 |
 +--< AuthenticationIdentity
 |
 +--< WorkspaceMembership >-- Workspace
                                  |
                                  +--< WorkItem
                                         |
                                         +--< Subtask
                                         +--< Dependency
                                         +--< WorkSession
                                         +--< Attachment
                                         +--< ReminderPlan
```

## Important ownership distinction

A Work Item has:
- Created By
- Owner
- Assignee

These are distinct concepts.

Ownership transfer is authorized, audited, and event-producing.

## Deletion

Work Item deletion is soft deletion.

Default retention:
- 1 day

Retention is configurable.

Permanent cleanup is asynchronous.

Audit retention is separate from business-data retention.

## Attachments

Actual binary files live in object storage.

PostgreSQL stores metadata.

Default attachment limit:
- 2 MB

The limit is configurable.
