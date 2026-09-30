# Sprint 2 — Work Item Core

## Frozen decisions

- Every Work Item belongs to exactly one Workspace
- Created By, Owner, and Assignee are distinct
- Ownership transfer is authorized and audited
- Lifecycle: OPEN, IN_PROGRESS, COMPLETED, CANCELLED
- BLOCKED and DELAYED are orthogonal conditions
- Subtasks are one level deep
- Work Session is independent of Subtask
- Dependencies represent prerequisite relationships
- Soft delete is separate from lifecycle
- Completion with incomplete subtasks requires explicit confirmation and reason
- Reopen is allowed only within configurable window
- Cancellation requires reason
