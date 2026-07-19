# Domain — Secrets & Data Exposure

Hunt secrets leakage and sensitive-data exposure only. Shape adds stack probes.

## Hunt

- Hardcoded secrets; secrets in logs, errors, client bundles, or artifacts
- PII/payment minimization, encryption, retention boundaries
- Cookie flags (`HttpOnly`, `Secure`, `SameSite`); CORS; CSP; clickjacking
- Cache leakage; verbose stack traces to clients

## Checks

- Secrets live in a secret store or env — never committed or printed
- Browser-exposed env vars are intentionally public
- User-facing errors omit stack traces, SQL errors, tokens, and existence leaks
- Logs redact passwords, tokens, cookies, auth headers, card data, private prompts
- AuthZ failures and high-risk actions are audited with enough context
- Sensitive fields encrypted/tokenized/redacted where appropriate
- Exports authenticated, authorized, scoped, and audited
- Cache headers prevent private pages/API responses in shared caches
- CORS is not `*` with credentials; origins allowlisted
- `frame-ancestors` / `X-Frame-Options`, `nosniff`, HSTS in production

## Red flags

- Secrets in source maps, fixtures, CI logs, or frontend bundles
- Debug mode or verbose errors in production
- Private responses cached without tenant/user in the cache key
- PII or tokens sent to analytics or model providers unnecessarily
