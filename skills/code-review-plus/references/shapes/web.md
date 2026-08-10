# Shape — Web (PR review)

Hunt web-facing issues. Not a full threat model; deeper pass → `/deep-security-review`.

## Hunt for

- XSS: untrusted strings into HTML, attributes, or `innerHTML` / dangerous sinks without encoding
- CSRF: state-changing routes without CSRF token or equivalent when cookies authenticate the session
- Cookies: missing `Secure` / `HttpOnly` / `SameSite` on session or auth cookies set in this diff
- CORS: `Access-Control-Allow-Origin: *` (or echo of request Origin) combined with credentials
- Open redirects: user-controlled URL passed to redirect without allowlist

## Pass A

- Check global middleware before flagging a single route
- Defense-in-depth gaps are hardening (P2)
