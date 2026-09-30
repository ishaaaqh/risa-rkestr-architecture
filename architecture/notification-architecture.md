# Notification Architecture

Reminder Engine decides **WHEN**.

Notification System decides **HOW**.

## Flow

```text
Work Item
 + Classification
 + Time
 + Planning
       |
Reminder Policy Engine
       |
Reminder Plan
       |
Reminder Instance
       |
Notification Request
       |
Notification System
  +-- In-App
  +-- Push
  +-- Email
```

## Notification Request

Conceptually contains:
- Recipient
- Channel
- Template
- Data
- Priority
- Correlation ID
- Idempotency Key

## Lifecycle

Notification delivery:

PENDING → PROCESSING → DELIVERED

or:

PROCESSING → RETRYING → DELIVERED / FAILED

In-app read state is separate:

UNREAD → READ

Reminder history and notification history are separate concepts.
