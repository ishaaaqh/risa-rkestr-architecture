# Data Flow — Work Item Creation

```text
Next.js
  |
API
  |
Authentication
  |
Authorization
  |
Work Item Application Service
  |
Domain validation
  |
Classification / Decision Engine
  |
PostgreSQL transaction
  +-- Work Item
  +-- Audit where required
  +-- Outbox event
  |
Commit
  |
Response
  |
Async event processing
  +-- Reminder
  +-- Notification
  +-- Search/derived processing
  +-- Analytics
```
