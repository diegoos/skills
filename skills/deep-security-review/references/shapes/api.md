# Shape — API

REST, GraphQL, WebSocket, RPC, webhook, and public/internal API probes.
Pair with a domain file; do not re-hunt AuthZ/Injection generics already there.

## AuthN / token surface

- JWT: pin algorithms; verify iss, aud, exp, nbf, signature; no secrets in payload
- API keys hashed at rest, scoped, rate-limited, revocable
- Refresh tokens server-side or rotated; logout revokes them

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

- Import, avatar, link-preview, webhook callback, proxy destinations
- Block `169.254.169.254` and private ranges after DNS + redirects
- Timeouts, size, and content-type limits on fetches
