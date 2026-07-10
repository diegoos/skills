---
name: commit-message
description: >
  Create commit messages following the Conventional Commits specification based
  on the actual diff and staged files. Use only when you are asked to create a
  commit message. Do not use this skill for any other purpose.
---

# Git Commit with Conventional Commits

Operate in "Low Reasoning Effort" mode: focus on generating the commit message
from the diff and staged files. Terse and exact — no fluff. Why over what.

## Format

```text
<type>[scope]: <description>

[optional body]

[optional footer(s)]
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`,
`ci`, `chore`, `revert`.

- Subject ≤72 chars, imperative mood ("add" not "added"), no trailing period.
- Body only when the why is non-obvious, or for breaking changes / migrations.
  Wrap at 72 chars, bullets with `-`.
- Footers: `Closes #123`, `Refs #456`, `BREAKING CHANGE: ...`.
- Breaking change: `feat!:` or `BREAKING CHANGE:` footer.
- Match the project's language and style — determine by checking `git log --format=%B -5`.

## Workflow

### 1. Analyze the diff

```bash
git diff --staged          # prefer staged; fall back to working tree
git diff
git status --porcelain
```

### 2. Stage (if needed)

```bash
git add -A                 # or stage specific files/patterns/hunks
```

Never stage secrets (`.env`, keys, credentials).

### 3. Execute the commit — use heredoc

Heredoc avoids shell escaping issues and works across zsh/bash:

```bash
git commit -F <(cat << 'EOF'
<type>[scope]: <description>

- why this change, if not obvious.
- additional context.

Closes #123, Refs #456
EOF
)
```

Single-line fallback: `git commit -m "<type>[scope]: <description>"`. Avoid
`dquote>` interactive prompts and never use `-i`.

## What never goes in

- "This commit does X", "I", "we", "now", "currently" — the diff says what.
- AI attribution ("Generated with Claude", "Co-authored-by Claude") unless the
  project's own rule requires an AI-attribution trailer.
- Restating the filename when scope already says it.
- Emoji (unless project convention requires).
- Trailing notes like "All changes committed locally; no push performed."

## Safety protocol

- NEVER update git config, force push, or run destructive commands (`--force`,
  hard reset) without explicit request.
- NEVER skip hooks (`--no-verify`) unless the user asks.
- NEVER push or offer to push / open a PR — create the commit locally for
  review.
- NEVER commit secrets or sensitive files.
- If a commit fails (hook rejection, etc.), fix the issue and create a NEW
  commit — do not amend on the first attempt.

## Auto-Clarity

Always include a body for: breaking changes, security fixes, data migrations, or
reverts of prior commits. Never compress these into subject-only.

## Examples

```text
feat(api): add GET /users/:id/profile

Mobile client needs profile data without the full user payload to
reduce bandwidth on cold-launch screens.

Closes #128
```

```text
feat(api)!: rename /v1/orders to /v1/checkout

BREAKING CHANGE: clients on /v1/orders must migrate to /v1/checkout
before 2026-06-01. Old route returns 410 after that date.
```

```text
fix(auth): validate session before token refresh
```
