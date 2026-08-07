# Pipeline — Security

Hunt input validation, injection, auth gaps, and data exposure only.

For a deeper security pass, tell the user to invoke `/deep-security-review` (user-invoked only — do not auto-start it).

## Hunt for

- SQL/command/path injection, XSS, CSRF
- Hardcoded secrets, API keys, credentials in code or logs
- Missing input validation or sanitization at system boundaries
- Insecure defaults (permissive CORS, disabled CSRF, weak hashing)
- Authentication/authorization gaps on sensitive operations
- External data (APIs, user input, config) treated as untrusted
- Sensitive data exposure in logs, errors, or responses
- Dependency trust and known vulnerabilities

## Security-specific rules

- Check global middleware before flagging a route as missing CSRF/auth
- Classify data provenance: direct user input, LLM content, or backend value
- Evaluate the **final output** of sanitization pipelines, not one step
- Defense-in-depth gaps are hardening — not active vulnerabilities

## Pass A reminders

- Point to the exact line that makes the issue exploitable **today**
- `evidence_level` must be `proven` or `likely`
- Suggested fix: minimal and local; note `regression_risk` for auth contracts and shared middleware
