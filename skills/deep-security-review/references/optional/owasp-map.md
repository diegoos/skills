# Optional — OWASP Map

Load only when the user asks for an OWASP map, or the stack is unknown and the surface is public HTTP. Replaces slot 2 for AuthZ or Injection (still ≤2 files).
This file points — it does not rewrite domain/shape checks.

## Category → where to hunt

| OWASP theme | Primary domain | Shape hints |
| ----------- | -------------- | ----------- |
| Broken Access Control | `domains/authz.md` | `shapes/api.md`, `shapes/web.md` |
| Authentication Failures | `domains/authz.md` | language + `shapes/web.md` |
| Injection | `domains/injection.md` | language + `shapes/api.md` |
| Cryptographic Failures | `domains/secrets.md` | language + `shapes/cloud.md` |
| Security Misconfiguration | `domains/secrets.md` + `domains/infrastructure.md` | `shapes/cloud.md`, `shapes/web.md` |
| Software Supply Chain Failures | `domains/infrastructure.md` | `shapes/sensitive-flows.md`, `shapes/tooling.md` |
| Insecure Design | `domains/business-llm.md` | `shapes/sensitive-flows.md` |
| Integrity Failures | `domains/infrastructure.md` | `shapes/sensitive-flows.md` |
| Logging / Alerting Failures | `domains/secrets.md` | `shapes/cloud.md` |
| Exceptional Conditions | `domains/secrets.md` | language shapes |
| SSRF (2021) | `domains/injection.md` | `shapes/api.md`, `shapes/web.md` |

## Quick verification reminders

- User A cannot access user B resources (object-level)
- Non-admin cannot call admin endpoints (function-level)
- Injection payloads treated as data; output encoded for context
- Lockfiles + CI reproducible installs; secrets not in artifacts
