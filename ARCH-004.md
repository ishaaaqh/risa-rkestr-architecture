# ARCH-004 — Definition of Done & Engineering Workflow

## Objective

Establish the engineering contract for building Rkestr consistently across the architecture, backend, and frontend repositories.

## Artifacts

- Definition of Ready
- Definition of Done
- Engineering Workflow
- Repository Conventions
- Branching and Release Policy
- Architecture Change Policy
- Ticket Template

## Core principle

**Architecture → Contract → Implementation → Verification → Release**

Significant architectural decisions must be explicit, reviewable, documented, and traceable to implementation.

## Definition of Done

A ticket is complete only when applicable functional, engineering, security, reliability, observability, documentation, and verification requirements are satisfied.

## Workflow

BACKLOG → READY → IN PROGRESS → REVIEW → VALIDATION → DONE

## Cross-repository traceability

Business ticket → Architecture ticket → Backend/Frontend implementation → Verification.

## Definition of Ready

Implementation begins only when intent, scope, acceptance criteria, dependencies, architecture impact, and relevant security/data/API/event implications are understood.

## Architecture changes

Architecture changes require an ADR and corresponding documentation/diagram updates before implementation continues.

## Branching

Default:

`feature/* → develop → main`

Protected branches require review and passing CI.

## Secrets

Real secrets are never committed to source control.

## Database

Versioned migrations are mandatory. Prefer expand → migrate → contract for rolling deployments.

## Release

Reviewed changes, passing CI, migration compatibility, configuration readiness, rollback consideration, and observability are required for release.

## Status

ARCH-004 closes the architecture/process foundation and establishes the engineering operating model for implementation.
