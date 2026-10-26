# Shape — API

REST, GraphQL, WebSocket, RPC, webhook, and public/internal API probes.
Pair with a domain file. JWT verification defects → `domains/authz.md` (do not restate).

## AuthN / token surface

- API keys hashed at rest, scoped, rate-limited, revocable
- Refresh tokens server-side or rotated; logout revokes them
- Stack-specific JWT wiring only (library calls, middleware order) — defect rules live in authz

## API-specific AuthZ probes

- Webhook signature validation before side effects
- GraphQL: field-level AuthZ on resolvers; limit depth/batching
- Background jobs carry tenant/actor; deferred work cannot escalate

## API injection / abuse probes

- GraphQL introspection in production, nested query DoS, alias batching
- NoSQL operator injection via JSON bodies (`$ne`, `$gt`, nested ops)
- Sort/filter field allowlists on list endpoints
- Rate limits: login, reset, MFA, refresh, signup, search, export, upload, webhooks

## SSRF / callbacks

- Import, avatar, link-preview, webhook callback, proxy destinations (SSRF policy → injection.md)
- Timeouts, size, and content-type limits on fetches
