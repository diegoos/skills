# Shape — Cloud & Infrastructure

IAM, CI/CD, containers, IaC, CDN. Pair with domain-infrastructure. Policy lives in the domain; this file holds concrete probes.

## IAM

- No root for routine ops; MFA for privileged users
- Service accounts least privilege; no wildcards like `*:*` / broad `iam:*`
- Long-lived creds avoided/rotated; break-glass documented
- Prod and staging do not share credentials or databases

## Secrets in CI/deploy

- Secrets in platform secret store; `.env` / key files gitignored
- Fork PRs cannot read production secrets
- Build steps do not echo env; artifacts exclude `.env` and key JSON
- Client-exposed env vars intentionally public

## Network / containers / edge

- Only required ports public; DBs/queues/admin panels private
- TLS enforced; trust `X-Forwarded-*` only from known infra
- Minimal images; non-root; read-only FS where practical
- CDN cache keys include auth/tenant; private `Cache-Control`
- Host-header constrained for password-reset / absolute URL generation
- SRI (or equivalent) for third-party CDN scripts; private buckets by default

## CI/CD

- Branch protection + required reviews for production
- Deploy permissions separated by environment (SoD)
- Workflows avoid shelling untrusted PR data
- Third-party actions pinned to SHA; attestations verified before deploy when available
- Encryption at rest for DBs/object storage; unsigned update channels flagged
