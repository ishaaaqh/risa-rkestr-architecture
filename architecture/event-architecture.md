# Event Architecture

## Flow

```text
User action
  |
Domain transaction
  |
PostgreSQL state + Outbox event
  |
Event Publisher
  |
Message Broker
  |
Consumers
  +-- Reminder
  +-- Notification
  +-- Analytics
  +-- Future integrations
```

## Outbox

The domain state change and outbox event are committed in the same transaction.

This prevents lost events.

## Event metadata

Events should contain:
- Event ID
- Event Type
- Event Version
- Occurred At
- Producer
- Correlation ID
- Causation ID
- Workspace ID
- Actor/User ID
- Payload

## Delivery

At-least-once delivery is the target.

Exactly-once delivery is not assumed.

Consumers must be idempotent.

## Reliability

- Retry transient failures
- Exponential backoff
- Jitter
- Dead Letter Queue
- Poison-message isolation
- Business-key ordering where required

Todo/Work Item events should generally preserve ordering by Work Item ID rather than imposing global ordering.
