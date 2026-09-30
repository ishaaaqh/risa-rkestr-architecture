# Frontend Architecture

## Technology

- Next.js
- React
- TypeScript

## Feature-oriented organization

```text
features/
  auth/
  workspace/
  workitem/
  reminders/
  notifications/
  search/
  productivity/
```

Shared concerns live separately:

```text
components/
hooks/
services/
types/
lib/
styles/
```

## Principle

The frontend should be organized around user capabilities and workflows rather than a flat collection of components.

## User experience

Rkestr should expose:
- Today
- Upcoming
- Overdue
- Delayed
- Important
- Delegated
- Blocked
- Eisenhower Matrix
- Saved Views
- Workspace views

The UI must never be treated as the security boundary. Backend authorization remains authoritative.
