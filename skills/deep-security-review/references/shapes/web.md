# Shape — Web Application

Browser-facing apps, SPA, SSR, admin panels. Pair with a domain file.

## Browser XSS / HTML

- Escape by default; raw HTML uses conservative sanitizer
- Markdown/SVG/rich text treated as active content
- Dangerous sinks: `innerHTML`, `outerHTML`, `insertAdjacentHTML`, framework raw HTML
- CSP present; avoid broad `unsafe-inline` / `unsafe-eval` unless justified
- URLs reject `javascript:` / unsafe `data:`

## CSRF / cookies / headers

- CSRF tokens or same-origin checks for high-impact cookie mutations
- Cookies: `HttpOnly`, `Secure`, appropriate `SameSite`
- Session rotation after login and privilege change
- CORS: no `*` with credentials; origin allowlist
- `frame-ancestors` / `X-Frame-Options`, `nosniff`, HSTS, safe referrer policy

## Uploads / redirects / realtime

- Upload validation beyond client MIME; store outside executable paths
- Archive extraction: zip slip, symlink, decompression bombs
- Open redirect and OAuth redirect URI allowlists
- WebSockets: auth on connect/reconnect; per-channel AuthZ; message limits

## Cache / host / smuggling (when topology suggests)

- Trust in `Host` / `X-Forwarded-*` for password-reset or absolute URLs
- Cache keys omit auth/tenant/locale → cross-user cache poisoning risk
- Mixed proxies / custom body parsing → flag for deployment verification
