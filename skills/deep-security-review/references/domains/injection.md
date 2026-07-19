# Domain — Injection & Input Boundaries

Hunt injection and untrusted-input sinks only. Shape file adds stack probes.

## Hunt

- SQL/NoSQL/command/LDAP/template/path injection; XSS; CSRF
- SSRF, XXE, unsafe deserialization, file-upload trust (MIME vs content)
- Schema/allowlist validation before business logic
- URL fetchers reaching private IPs, metadata endpoints, or non-HTTP schemes

## Checks

- Bodies, params, query, headers, cookies validated at runtime with allowlists
- Unknown fields rejected or stripped on mutations
- Database access parameterized or via safe ORM APIs
- Shell commands never interpolate user input; prefer direct APIs
- Paths normalized and confined to an allowed base directory
- Uploads constrained by size, extension, content type, and content where relevant
- URL fetch: allow expected schemes; block private/metadata after DNS + redirects
- Output encoded for the correct context (HTML, attribute, URL, JS, JSON)
- CSRF protection for cookie-authenticated state changes (or equivalent)

## Specific probes

- Injection in filters, IDs, search, sort, JSON bodies
- Command injection in import/export, image/PDF/archive processing
- Path traversal in download, template selection, localization, asset proxying
- Mass-assignment of privileged fields on valid payloads
- GraphQL introspection, deep nesting, batching, resolver AuthZ gaps
- SSRF via avatars, link previews, webhooks, import URLs, callbacks
