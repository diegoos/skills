# Domain — Authentication & Authorization

Hunt AuthN/AuthZ only. Shape file (if any) adds stack-specific probes.

## Hunt

- Session, JWT, OAuth/OIDC, API-key handling; MFA; password storage
- Object-level and function-level access control; tenant isolation; IDOR/BOLA
- Ownership checks next to the operation (Middleware alone is not AuthZ)
- Privilege escalation via mass assignment (`role`, `tenantId`, `isAdmin`, price)

## Checks

- Protected endpoints reject anonymous callers
- Identity comes from the session/token, not request body fields
- Resource lookup includes owner, tenant, or organization constraints
- Admin-only actions check role/permission at handler or service layer
- List endpoints scope results server-side; client filters are not AuthZ
- Webhooks authenticate the sender before side effects
- Background jobs preserve tenant and actor context
- Tokens expire; refresh tokens are revocable or rotated
- Passwords use adaptive hashing; never logged
- Login, reset, MFA, and refresh have brute-force protection

## Red flags

- `findUnique({ id })` then return before ownership check
- Accepting `tenantId` / `userId` / `role` / `isAdmin` from clients
- Authorization only in UI or frontend routes
- Service functions callable without actor or tenant parameter
- Helper named `auth()` treated as authorization without ownership proof
