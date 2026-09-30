# Repository Conventions

## Repositories

- `risa-rkestr-architecture`
- `risa-rkestr-backend`
- `risa-rkestr-frontend`

## Branching

Initial workflow:

```text
feature/*
   ↓
develop
   ↓
main
```

Feature branch examples:

- `feature/AUTH-001-user-domain`
- `feature/WORK-001-workspace`
- `feature/WORKITEM-001-create-work-item`

## Secrets

Never commit real secrets.

Use:
- `.env.example`
- environment variables locally
- managed secret storage in deployed environments

## Commit style

Use clear, ticket-referenced commits where practical:

`AUTH-001 Add user identity foundation`

## Cross-repository traceability

A business story may map to architecture, backend, frontend, and test tasks.

Example:

```text
AUTH-001 User Registration
 ├── AUTH-001-ARCH
 ├── AUTH-001-BE
 ├── AUTH-001-FE
 └── AUTH-001-TEST
```
