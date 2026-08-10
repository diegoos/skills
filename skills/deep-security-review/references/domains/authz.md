# Domain — Authentication & Authorization

Hunt AuthN/AuthZ only. Shape file (if any) adds stack-specific probes. JWT verification defects live here (not in `api.md`).

## Hunt

- Session, JWT, OAuth/OIDC, API-key handling; MFA; password storage
- Object-level and function-level access; tenant isolation; IDOR/BOLA
- Ownership next to the operation (middleware alone is not AuthZ); deny-by-default
- Privilege escalation via mass assignment (`role`, `tenantId`, `isAdmin`, price)
- Alternate paths / force browsing: admin vs user routes, legacy endpoints, IDOR twins
- Fail-open / error-path AuthZ; batch/export/import/preview per-item checks

## Checks

- Protected endpoints reject anonymous callers; missing allow → deny
- Identity from session/token, not request body; resource lookup includes owner/tenant/org
- Admin actions check role/permission at handler or service layer
- List endpoints scope server-side; client filters are not AuthZ
- Webhooks authenticate sender; background jobs preserve tenant/actor
- Tokens expire; refresh revocable/rotated; logout/SLO invalidates sessions and tokens
- Passwords: adaptive hashing, never logged; uniform messaging on auth failures
- Login/reset/MFA/refresh: brute-force, stuffing/spray, breached-password defense
- Reset tokens: binding, entropy, Host-header safe; MFA fallback cannot skip step-up
- JWT: pin algorithms; verify signature before use; check iss/aud/exp/nbf; reject `alg` confusion and decode-without-verify; constrain `kid`/`jku`/`x5u`
- Auth dependency errors on protected requests deny (fail-closed), not allow
- Batch/export/import/preview enforce per-item ownership/tenant, not only list AuthZ

## Red flags

- `findUnique({ id })` then return before ownership check
- Accepting `tenantId` / `userId` / `role` / `isAdmin` from clients
- Authorization only in UI or frontend routes
- Service functions callable without actor or tenant parameter
- Helper named `auth()` treated as authorization without ownership proof
- Catch-all that grants access when AuthZ lookup throws or times out
