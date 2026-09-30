# API Governance

## Versioning

Base path:

`/api/v1`

## Requirements

- Consistent resource naming
- Validation
- Consistent error contract
- Correlation/request IDs
- Pagination
- Filtering
- Sorting
- Idempotency where appropriate
- Backward compatibility
- Explicit authorization

## Errors

Errors should be machine-readable and human-understandable.

The API should expose a stable error structure containing enough information for clients and observability without leaking sensitive internals.

## Contracts

OpenAPI will become the formal API contract as implementation progresses.
