# Architecture Change Policy

Architecture is changed deliberately.

## Change triggers

An ADR is required when a change affects:

- Major runtime topology
- Module boundaries
- Persistence strategy
- Authentication/authorization model
- Event contracts
- Messaging semantics
- Consistency guarantees
- API versioning strategy
- Deployment strategy
- Security architecture
- Significant reliability/scalability behavior

## Change sequence

1. Identify the problem.
2. Document constraints.
3. Record options.
4. State the decision.
5. Record consequences.
6. Update affected architecture documents.
7. Update diagrams.
8. Link implementation tickets.

## Principle

Implementation must not silently become the architecture source of truth.
