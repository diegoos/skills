# Shape — Cloud & Infrastructure

IAM, CI/CD, containers, IaC, CDN. Pair with domain-infrastructure.

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

## CI/CD

- Branch protection + required reviews for production
- Deploy permissions separated by environment
- Workflows avoid shelling untrusted PR data
- Third-party actions pinned to SHA/version when risk warrants
- Encryption at rest for DBs/object storage; private buckets by default
