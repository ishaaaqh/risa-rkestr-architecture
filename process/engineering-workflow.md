# Engineering Workflow

## 1. Architecture first

For architecture-affecting work:

Architecture decision → ADR/documentation → diagram update → implementation.

Do not introduce significant architecture through application code first.

## 2. Ticket flow

Recommended lifecycle:

BACKLOG → READY → IN PROGRESS → REVIEW → VALIDATION → DONE

BLOCKED may be applied whenever external dependency or unresolved decision prevents progress.

## 3. Cross-repository traceability

Use a shared business ticket ID.

Example:

- `AUTH-001` — business story
- `AUTH-001-ARCH` — architecture
- `AUTH-001-BE` — backend
- `AUTH-001-FE` — frontend
- `AUTH-001-TEST` — verification

Pull requests reference the relevant ticket IDs.

## 4. Implementation sequence

When a change crosses layers:

1. Architecture / contract
2. Backend
3. Database migration if required
4. Tests
5. Frontend
6. Integration verification
7. Documentation

The exact sequence may vary when a ticket explicitly requires another approach.

## 5. Pull requests

Every PR should include:

- What changed
- Why it changed
- Ticket reference
- Architectural impact
- API/data/event impact
- Test evidence
- Security considerations
- Migration/configuration considerations
- Rollback considerations when relevant

PRs should be small enough to review meaningfully.

## 6. Branching

Default:

feature/* → develop → main

Hotfixes may branch from main and merge back into main and develop as appropriate.

Protected branches require review and passing CI.

## 7. Commits

Use concise conventional-style commits.

Examples:

- `feat(auth): add password login`
- `fix(work-item): validate deadline ordering`
- `docs(architecture): add reminder flow`
- `test(auth): add session revocation tests`

Avoid mixing unrelated changes in one commit.

## 8. Architecture changes

If implementation reveals that an approved decision must change:

1. Stop the affected implementation path.
2. Record the proposed change.
3. Update/create ADR.
4. Update affected architecture documentation.
5. Update diagrams.
6. Resume implementation using the new decision.

Never silently drift from approved architecture.

## 9. Database changes

Use versioned migrations.

Prefer:

expand → migrate → contract

for changes that must support rolling deployments.

Never rely on manual production schema changes.

## 10. Release discipline

Production releases must have:

- Passing CI
- Reviewed changes
- Database migration compatibility
- Configuration/secrets verified
- Rollback/recovery consideration
- Observability ready
- Release/version recorded
