# Domain — Infrastructure & Supply Chain

Hunt infra, CI/CD, deps, and abuse controls. Shape adds cloud/tooling/sensitive probes.

## Hunt

- IAM, network exposure, CI/CD permissions, env/config secrets handling
- Dependency risk, lockfile integrity, package publish trust
- Rate limiting / brute-force / replay on abuse-prone endpoints
- Containers, edge/CDN, deployment defaults

## Checks

- Service accounts least privilege; no wildcard `*:*` for routine ops
- Long-lived credentials avoided or rotated; MFA for privileged users
- Public services expose only required ports; DBs/queues not internet-exposed
- Lockfiles committed; CI uses reproducible installs
- Critical/high dependency vulns fixed or risk-accepted
- Fork PRs cannot read production secrets or publish/deploy
- CI tokens minimum permissions; third-party actions pinned when risk warrants
- Rate limits on login, reset, MFA, search, export, upload, LLM/tool calls
- Containers non-root when practical; minimal base images
- CDN/cache keys include auth/tenant where needed; private `Cache-Control`

## Red flags

- Static cloud credentials in repo or unrotated CI vars
- Staging and production share credentials or databases
- Install/postinstall scripts that can exfiltrate secrets
- Admin endpoints public without auth or IP restriction
