# ADR-001 — Modular Monolith First

## Status
Accepted

## Context
Rkestr is an enterprise-grade system but is initially being built by a small engineering team. Premature microservices would add operational complexity without a demonstrated need.

## Decision
Start with a Modular Monolith with strong internal module boundaries.

## Consequences
Positive:
- Simpler development
- Strong consistency
- Lower infrastructure overhead
- Easier debugging
- Future extraction remains possible

Negative:
- Requires discipline to maintain module boundaries
- Some modules may eventually need extraction
