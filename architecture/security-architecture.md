# Security Architecture

## Authorization chain

```text
Request
 |
Authentication
 |
User Identity
 |
Workspace Membership
 |
Permission
 |
Resource Ownership / Visibility
 |
Business Rule
 |
Operation
```

## Workspace boundary

Workspace is the user-facing tenant/security boundary.

Every workspace-owned resource must enforce membership and authorization.

## Visibility

- PRIVATE
- WORKSPACE
- DELEGATED

## RBAC

```text
User
 |
Workspace Membership
 |
Role
 |
Permission
```

Initial roles:
- PERSONAL: OWNER
- FAMILY: ADMIN, MEMBER
- WORK: ADMIN, MEMBER

Future roles may include MANAGER, CONTRIBUTOR, VIEWER.

## Security controls

- Adaptive password hashing
- Token/session revocation
- Password reset expiration
- Authentication rate limiting
- Resource-level authorization
- Input validation
- Security headers
- TLS in production
- Encryption at rest
- Externalized secrets
- Security event audit
- Dependency and container scanning
