# Optional — OWASP Map

Load when the user asks for an OWASP map, or the stack is unknown and the surface is public HTTP. Replaces slot 2 for AuthZ or Injection (still ≤2 files).

**Awareness map only — not a coverage standard.** Does not change the dispatch algorithm. This file points; it does not rewrite domain/shape checks.

[OWASP Top 10:2025](https://top10.owasp.org/2025/) · [Introduction](https://top10.owasp.org/2025/0x00_2025-Introduction/). A03 is broader than CVE/SCA. A10 is broader than AuthZ fail-open.

## Category → where to hunt

| ID        | OWASP theme                                                  | Primary domain                                                          | Shape hints                                      |
| --------- | ------------------------------------------------------------ | ----------------------------------------------------------------------- | ------------------------------------------------ |
| A01:2025  | Broken Access Control                                        | `domains/authz.md`                                                      | `shapes/api.md`, `shapes/web.md`                 |
| A07:2025  | Authentication Failures                                      | `domains/authz.md`                                                      | language + `shapes/web.md`                       |
| A05:2025  | Injection                                                    | `domains/injection.md`                                                  | language + `shapes/api.md`                       |
| A04:2025  | Cryptographic Failures                                       | `domains/secrets.md`                                                    | language + `shapes/cloud.md`                     |
| A02:2025  | Security Misconfiguration                                    | `domains/secrets.md` + `domains/infrastructure.md`                      | `shapes/cloud.md`, `shapes/web.md`               |
| A03:2025  | Software Supply Chain Failures                               | `domains/infrastructure.md`                                             | `shapes/sensitive-flows.md`, `shapes/tooling.md` |
| A06:2025  | Insecure Design                                              | `domains/business-llm.md`                                               | `shapes/sensitive-flows.md`                      |
| A08:2025  | Software or Data Integrity Failures                          | `domains/infrastructure.md`                                             | `shapes/cloud.md`, `shapes/sensitive-flows.md`   |
| A09:2025  | Security Logging and Alerting Failures                       | `domains/secrets.md`                                                    | `shapes/cloud.md`                                |
| A10:2025  | Mishandling of Exceptional Conditions                        | `domains/authz.md` + `domains/injection.md` + `domains/business-llm.md` | language shapes                                  |
| A01:2025  | SSRF (under Broken Access Control; hunt stays Injection)     | `domai ns/injection.md`                                                  | `shapes/api.md`, `shapes/web.md`                 |

## Quick verification reminders

- User A cannot access user B resources (object-level)
- Non-admin cannot call admin endpoints (function-level)
- Injection payloads treated as data; output encoded for context
- Lockfiles + CI reproducible installs; secrets not in artifacts
- Auth dependency errors deny on protected paths (fail-closed)
- Missing security audit/alert without exploit path → Verification Gaps (secrets domain)
