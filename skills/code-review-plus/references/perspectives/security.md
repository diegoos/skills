# Pipeline — Security

Hunt input validation, injection, auth gaps, and data exposure that are exploitable **today**.

## Hunt for

- SQL/command/path injection, XSS, CSRF
- Hardcoded secrets, API keys, credentials in code or logs
- Missing input validation or sanitization at system boundaries
- Insecure defaults (permissive CORS, disabled CSRF, weak hashing)
- Authentication/authorization gaps on sensitive operations
- External data (APIs, user input, config) treated as untrusted
- Sensitive data exposure in logs, errors, or responses
- Dependency trust and known vulnerabilities

## Pass A

Check global middleware before a route finding. Classify data provenance (user / LLM / backend). Judge the **final output** of a sanitization pipeline. Hardening without a path today stays category hardening. Report secrets as `file:line` + type only. Note `regression_risk` for auth contracts and shared middleware.
