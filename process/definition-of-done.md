# Definition of Done

A ticket is Done only when all applicable criteria are satisfied.

## Functional
- Acceptance criteria pass.
- Business rules are implemented.
- Validation and authorization are enforced server-side.
- Error behavior follows the API contract.

## Engineering
- Code follows repository conventions.
- Automated tests cover important behavior.
- No known critical/high defect remains from the change.
- Database migrations are versioned and repeatable where applicable.
- Idempotency/concurrency is handled where required.

## Security
- Authentication/authorization implications reviewed.
- Sensitive data is not logged.
- Secrets are not committed.
- Input validation and resource-level authorization are verified.

## Reliability
- External failures do not corrupt authoritative state.
- Async consumers are idempotent where applicable.
- Retry/DLQ behavior is defined where applicable.

## Observability
- Logs, metrics, traces, correlation IDs, and audit events are added where appropriate.
- Operationally important failures are diagnosable.

## Documentation
- API, architecture, ADR, data model, or flow documentation is updated when affected.

## Verification
- Build passes.
- Relevant automated tests pass.
- Static/security checks pass where configured.
- Reviewer approval is obtained.
- Changes are merged using the repository workflow.
