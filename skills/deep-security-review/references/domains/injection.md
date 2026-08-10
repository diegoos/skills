# Domain — Injection & Input Boundaries

Hunt injection and untrusted-input sinks only. Shape file adds stack probes. Prompt injection → BusinessLLM domain.

## Hunt

- SQL/NoSQL/command/LDAP/template/path injection; XSS; CSRF; SSTI/EL/OGNL
- SSRF (allowlist + redirects + DNS rebind/TOCTOU); XXE; unsafe deserialization; uploads
- Schema/allowlist validation before business logic; second-order (store then later sink)
- URL fetchers reaching private IPs, metadata endpoints, or non-HTTP schemes

## Checks

- Bodies, params, query, headers, cookies validated at runtime with allowlists
- Unknown fields rejected or stripped on mutations (mass-assignment AuthZ lives in authz.md)
- Database access parameterized or via safe ORM APIs; no raw concat of user input
- Dynamic identifiers / `ORDER BY` / table names allowlisted (see language shapes)
- Shell commands never interpolate user input; prefer direct APIs
- Paths normalized and confined to an allowed base directory
- Uploads constrained by size, extension, content type, and content where relevant
- SSRF: allow expected schemes/hosts; re-resolve after redirects; block private/metadata after DNS (rebind/TOCTOU)
- Output encoded for the correct context (HTML, attribute, URL, JS, JSON)
- CSRF protection for cookie-authenticated state changes (or equivalent)
- Template/expression engines: user input never reaches EL/OGNL/SSTI evaluation
- Second-order: untrusted data stored then reused at a sink — both halves proven

## Specific probes

- Injection in filters, IDs, search, sort, JSON bodies
- Command injection in import/export, image/PDF/archive processing
- Path traversal in download, template selection, localization, asset proxying
- GraphQL introspection, deep nesting, batching, resolver AuthZ gaps
- SSRF via avatars, link previews, webhooks, import URLs, callbacks
