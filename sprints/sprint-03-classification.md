# Sprint 3 — Classification & Decision Engine

## Classification dimensions

- Context
- Category
- Priority
- Importance
- Urgency
- Task Nature

## Task Nature

- IMMEDIATE
- EFFORT_BASED

## Decision Engine

High importance + high urgency → DO NOW

High importance + low urgency → SCHEDULE

Low importance + high urgency → DELEGATE

Low importance + low urgency → LOW ATTENTION

The quadrant is derived and not persisted as an independent user classification.

Importance and urgency are explicitly user-controlled for MVP.

The system may suggest changes but cannot silently override them.
