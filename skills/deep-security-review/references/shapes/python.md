# Shape — Python

Django, FastAPI, Flask, scripts, jobs. Pair with a domain file.
Type hints are not runtime validation.

## Validation & injection

- Pydantic / Marshmallow / Django forms / FastAPI models at boundaries
- Parameterized SQL/ORM; no string-built query fragments or sort fields
- No user input into `eval`, `exec`, dynamic imports, or expression evaluators
- Template escaping on by default

## Deserialization & shell

- Never `pickle` / `marshal` on untrusted data
- `yaml.load` only with `SafeLoader`
- `subprocess` without `shell=True`; argument arrays, not string interpolation
- Temp files and path canonicalization for user filenames

## Framework & crypto

- Debug mode off in production; `ALLOWED_HOSTS` / CORS restricted
- CSRF enabled for cookie-authenticated mutations
- Session cookies `HttpOnly` / `Secure` / `SameSite`
- Secret keys per environment, not framework defaults
- Passwords: Argon2 / bcrypt / PBKDF2 / framework hashers
- TLS verification not disabled in HTTP clients

## Dependencies

- Locked/pinned deps; `pip-audit` / Safety / Snyk or CI equivalent
- Bandit / Semgrep / Ruff security rules where available
