# Sprint 4 — Deadlines & Time Semantics

## Temporal concepts

- Created At
- Updated At
- Planned Start
- Soft Deadline
- Hard Deadline
- Completed At
- Cancelled At

## Deadline status

UPCOMING → DUE_SOON → DUE → OVERDUE → DELAYED

OVERDUE means the deadline passed.

DELAYED means the Work Item remains incomplete beyond the configured grace period.

All-day tasks are represented as local calendar dates rather than invented midnight semantics.

Authoritative timestamps are stored in UTC.

Timezone precedence:
1. Explicit Work Item timezone where needed
2. Workspace timezone
3. User timezone
4. System default
