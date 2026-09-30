# ADR-002 — Workspace as Security Boundary

## Status
Accepted

A User can belong to multiple Workspaces.

Authorization is evaluated through:

User → Workspace Membership → Role → Permission → Resource visibility/business rule.

Workspace-owned resources must enforce membership and authorization.
