# Sprint 1 — Identity, Workspace & Authorization

## Goal

Build the authentication, user, workspace, membership, role, permission, and invitation foundation.

## Backend-first vertical slices

1. User identity
2. Registration
3. Login
4. Sessions / token lifecycle
5. Password reset
6. Workspace
7. Membership
8. Roles and permissions
9. Authorization enforcement
10. Invitations

Each slice follows:

Architecture → Backend → Backend tests → API contract → Frontend → UI integration → E2E verification.

## Frozen decisions

- Hybrid authentication: email/password first, OIDC-ready
- Immutable internal User ID
- Email is an attribute, not permanent identity
- Multiple authentication identities supported by design
- Authentication and authorization are separate
- Workspace is the security boundary
- Roles are workspace-scoped
- Removing membership does not delete the User
- Invitation lifecycle: PENDING → ACCEPTED / EXPIRED / REVOKED
