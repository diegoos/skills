# Domain — Secrets & Data Exposure

Hunt secrets leakage, crypto policy, and sensitive-data exposure. Browser exploitation (DOM XSS, postMessage, clickjacking, CORS attack paths) lives in `shapes/web.md`.

## Hunt

- Hardcoded secrets; secrets in logs, errors, client bundles, or artifacts
- PII/payment minimization, encryption, retention boundaries
- Cookie flags (`HttpOnly`, `Secure`, `SameSite`); transport/header hygiene
- Cache leakage of private responses; verbose stack traces to clients
- Crypto: AEAD preferred; unique IV/nonce; no MD5/SHA1/ECB for security properties

## Checks

- Secrets live in a secret store or env — never committed or printed
- Browser-exposed env vars are intentionally public
- User-facing errors omit stack traces, SQL errors, tokens, and existence leaks
- Logs redact passwords, tokens, cookies, auth headers, card data, private prompts
- AuthZ failures and high-risk actions are audited with enough context
- Sensitive fields encrypted/tokenized/redacted where appropriate
- Exports authenticated, authorized, scoped, and audited
- Cache headers prevent private pages/API responses in shared caches
- Incomplete security headers without an exploit path → hardening note, not a vulnerability
- Missing security audit/alert on auth failures or high-risk actions without an exploit path → Verification Gaps (not Findings P0–P3)
- On any secret leak: rotate-first, then investigate scope

## Red flags

- Secrets in source maps, fixtures, CI logs, or frontend bundles
- Debug mode or verbose errors in production
- Private responses cached without tenant/user in the cache key
- PII or tokens sent to analytics or model providers unnecessarily
- Static IV/nonce reuse, ECB mode, or MD5/SHA1 used as a security control
