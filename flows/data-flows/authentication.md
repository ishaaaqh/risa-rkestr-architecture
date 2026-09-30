# Data Flow — Authentication

```text
Browser
  |
Next.js
  |
POST /api/v1/auth/...
  |
Identity module
  |
User + Authentication Identity
  |
Authentication session
  |
Access token + Refresh token
  |
Client
```

Authentication establishes identity.

Authorization is separately evaluated against Workspace Membership, Role, Permission, and resource rules.
