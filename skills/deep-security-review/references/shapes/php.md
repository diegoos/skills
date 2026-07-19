# Shape — PHP

Laravel, Symfony, WordPress, Composer APIs. Pair with a domain file.

## Configuration

- Production: `display_errors` off; no verbose stack traces
- `expose_php` disabled where practical
- Upload/body/memory/timeout limits set
- `.env`, backups, dumps, Composer artifacts not web-accessible

## PHP-specific sinks

- Prepared statements / safe ORM; no concat into `ORDER BY` / `LIMIT` / table names
- Templates escape by default; raw helpers rare and reviewed
- CSRF tokens on cookie-authenticated state changes
- Session rotate after login; logout invalidates server session
- Passwords via `password_hash` / `password_verify`

## Filesystem & RCE

- No `include`/`require`/`fopen`/`readfile` with raw request params
- Uploads outside executable paths; no executable uploaded PHP
- Never `unserialize` on untrusted data
- Avoid `eval`, string `assert`, `shell_exec`/`exec`/`system`/`passthru`
- Legacy `preg_replace` executable patterns absent

## Composer

- `composer.lock` committed; `composer audit` in process
- Post-install scripts understood for high-risk deploys
