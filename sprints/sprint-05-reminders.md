# Sprint 5 — Reminder Engine

Reminder Engine decides WHEN.

Notification System decides HOW.

## Policy hierarchy

1. Mandatory Workspace Policy
2. Explicit Work Item Reminder
3. Work Item-specific Policy
4. Workspace Default
5. System Default

## Strategies

- IMMEDIATE
- REPEATED
- IMPLEMENTATION_PROGRESS
- CUSTOM

Notification snooze changes notification timing only. It does not change Work Item deadline or lifecycle.

Completing a Work Item cancels pending reminders.
