# Data Flow — Event Processing

```text
Domain Command
 |
Database Transaction
 +-- Authoritative state
 +-- Outbox Event
 |
Event Publisher
 |
Message Broker
 |
Consumer
 |
Idempotency check
 |
Processing
 |
SUCCESS

or

FAILURE
 |
Retry with backoff
 |
DLQ after configured maximum
```

At-least-once delivery is assumed.
