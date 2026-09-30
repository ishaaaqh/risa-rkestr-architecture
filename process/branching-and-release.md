# Branching, Review & Release Policy

## Branches

- `main`: production-ready
- `develop`: integration branch
- `feature/<ticket>-<short-name>`: feature work
- `fix/<ticket>-<short-name>`: defect work
- `hotfix/<ticket>-<short-name>`: urgent production correction

## Merge requirements

At minimum:

- PR review
- CI green
- Tests passing
- No unresolved critical security finding
- Ticket linked

## Release

Use semantic versioning where a released API/library requires it:

- MAJOR — incompatible contract change
- MINOR — backward-compatible capability
- PATCH — backward-compatible correction

API evolution must preserve backward compatibility within `/api/v1` unless an explicit versioning decision is approved.

## Rollback

Application rollback must not assume database rollback.

Prefer backward-compatible database migrations and expand/migrate/contract patterns.
