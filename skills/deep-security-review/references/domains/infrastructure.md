# Domain — Infrastructure & Supply Chain

Hunt infra, CI/CD, deps, and abuse controls. Shape adds cloud/tooling/sensitive probes.

## Hunt

- IAM, network exposure, CI/CD permissions, env/config secrets handling
- Dependency risk by reachability (prod vs devDependency); lockfile integrity; transitive upgrades
- Install/publish trust; unsigned updates; CI SoD / identity ≤ runtime privilege
- Rate limiting / brute-force / replay on abuse-prone endpoints
- Containers, edge/CDN/SRI, storage ACLs, unnecessary surface

## Checks

- Service accounts least privilege; no wildcard `*:*` for routine ops
- Long-lived credentials avoided or rotated; MFA for privileged users
- Public services expose only required ports; DBs/queues not internet-exposed
- Lockfiles committed; CI uses reproducible installs; triage unmaintained deps
- Critical/high dependency vulns fixed or risk-accepted; note transitive risk on upgrades
- Fork PRs cannot read production secrets or publish/deploy
- CI tokens minimum permissions; identity used in CI ≤ runtime identity
- Verify-before-use: pin third-party actions by SHA; check attestations when available
- Rate limits on login, reset, MFA, search, export, upload, LLM/tool calls
- Containers non-root when practical; minimal base images
- CDN/cache keys include auth/tenant; private `Cache-Control`; SRI for third-party scripts
- Object storage private by default; unsigned update channels flagged
- Admin/debug endpoints not on the public surface without auth or network restriction

## Red flags

- Static cloud credentials in repo or unrotated CI vars
- Staging and production share credentials or databases
- Install/postinstall scripts that can exfiltrate secrets
- Admin endpoints public without auth or IP restriction
- CI identity that can deploy _and_ mutate production secrets without separation
