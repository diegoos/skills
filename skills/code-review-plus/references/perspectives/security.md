# Pipeline — Security

Hunt input validation, injection, auth gaps, and data exposure.

Deeper threat modeling: tell the user to invoke `/deep-security-review` (see skill Relation; do not auto-start).

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
- Defense-in-depth gaps are hardening (P2)
- Report secrets as `file:line` and secret type only; redact the value
- Suggest `/deep-security-review` when the surface needs threat modeling beyond this pass

## Pass A reminders

- Note `regression_risk` for auth contracts and shared middleware
