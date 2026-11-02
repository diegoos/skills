# Shape — Web Application

Browser-facing apps, SPA, SSR, admin panels. Pair with a domain file. Owns browser exploitation; Secrets owns transport/header hygiene without exploit path.

## Browser XSS / HTML

- Escape by default; raw HTML uses conservative sanitizer
- Markdown/SVG/rich text treated as active content
- Dangerous sinks: `innerHTML`, `outerHTML`, `insertAdjacentHTML`, framework raw HTML
- DOM XSS: trace source→sink; prefer escape-hatch-first (where encoding is skipped)
- CSP present; avoid broad `unsafe-inline` / `unsafe-eval` unless justified
- URLs reject `javascript:` / unsafe `data:`

## CSRF / cookies / origin

- CSRF tokens or same-origin checks for high-impact cookie mutations
- Cookies: `HttpOnly`, `Secure`, appropriate `SameSite`; session rotation after login/privilege change
- CORS: reflection + credentials is a vuln; no `*` with credentials; origin allowlist
- `postMessage`: verify `event.origin` (and source) before trusting data
- Clickjacking: report only when a sensitive action is frameable

## Uploads / redirects / realtime

- Upload validation beyond client MIME; store outside executable paths
- Archive extraction: zip slip, symlink, decompression bombs
- Open redirect and OAuth redirect URI allowlists
- WebSockets: Origin + token on connect/reconnect; per-channel AuthZ; message limits

## Cache / host / smuggling (when topology suggests)

- Host trust for password-reset or absolute URLs with cross-user impact
- Cache deception (unauthenticated URL caches authenticated content) vs cache poisoning (key omits auth/tenant)
- Mixed proxies / custom body parsing → lead with **needs-runtime**
