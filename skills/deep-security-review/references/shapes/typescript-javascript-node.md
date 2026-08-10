# Shape — TypeScript / JavaScript / Node

TS/JS/Node/npm/browser/serverless. Pair with a domain file.
TypeScript types are not a security boundary. Crypto policy → `domains/secrets.md`.

## Runtime validation

- Schema validation at every trust boundary (Zod, Valibot, Yup, Joi, etc.)
- Unknown fields rejected/stripped on mutations
- Explicit constraints on numeric, enum, URL, email, ID, role, tenant fields

## Node sinks

- Body size limits configured
- Parameterized SQL/ORM; NoSQL filters reject unexpected `$` keys
- Prefer libraries over shell; if `child_process`, no shell interpolation
- No `eval` / `Function` / unsafe `vm` / unsafe templates
- Regex on user input checked for catastrophic backtracking
- URL fetchers block private/metadata networks and unsafe redirects (SSRF policy → injection.md)

## Prototype pollution

- Deep merges reject `__proto__`, `constructor`, `prototype`
- Recursive write into prototypes + reachable gadget required before reporting
- User JSON not merged into config, session, or AuthZ objects
- Query/body parsers configured safely

## CSPRNG / secrets (JS-specific)

- Tokens, secrets, and nonces use `crypto.randomBytes` / `crypto.getRandomValues` — not `Math.random()`
- No long-lived tokens in `localStorage` / `sessionStorage`
- React `dangerouslySetInnerHTML` and dynamic script creation reviewed
- `NEXT_PUBLIC_*` / `VITE_*` / similar are public — never secrets
- Build artifacts and source maps free of secrets

## npm / runtime

- Lockfile + reproducible CI install; audit in process
- High-risk packages: parsers, auth, crypto, markdown/HTML, image/PDF/archive
- Current Node LTS; no debug/inspector in production; non-root containers
