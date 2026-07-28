---
name: commit-message
description: >-
  Create Conventional Commits from the real git status and diff. Use when asked to commit, write a commit message, or split changes into commits. Default: one atomic commit per concern; a single commit only when the user explicitly asks for one.
metadata:
  version: 0.2.0
  author: "Diego Oliveira"
  tags:
    - git
    - commit
    - conventional commits
    - commit message
---

# Git Commit with Conventional Commits

Terse and exact. Why over what. Prefer **atomic** commits — one concern each.

## Workflow

### 1. Survey

Run in parallel:

```bash
git status --porcelain
git diff --staged
git diff
git log --format=%B -5
```

Completion: every path in status is known, and recent commit language/style is known.

### 2. Partition

**Default — atomic:** Group every path from status into concerns. A concern is a distinct Conventional Commits `type`, `scope`, or intent (e.g. `feat` vs `fix` vs `docs`; two unrelated features; a refactor that only enables a feat). One group → one commit.

**Single-commit branch:** Collapse all safe paths into one group only when the user explicitly asks for a single commit (e.g. "one commit", "single commit", "só um commit"). Silence means atomic.

Exclude secrets and sensitive files from every group (`.env`, keys, credentials).

Completion: every path in status is in exactly one group, or excluded as secret/sensitive with that exclusion noted.

### 3. Stage, message, commit — once per group

For each group, in a sensible order (deps/infrastructure before dependents when it matters):

1. Stage **only** that group's paths (`git add -- path…`). Never `git add -A` while splitting.
2. Draft the message from that group's diff only — see Format.
3. Commit with heredoc:

```bash
git commit -F <(cat << 'EOF'
<type>[scope]: <description>

- why this change, if not obvious.

Closes #123
EOF
)
```

Single-line fallback when no body: `git commit -m "<type>[scope]: <description>"`. Never use `-i`.

On hook rejection: fix the issue and create a **new** commit for that group — do not amend on the first attempt.

Completion: every group has a successful commit; remaining status is empty or only the excluded secrets.

## Format

```text
<type>[scope]: <description>

[optional body]

[optional footer(s)]
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`.

- Subject ≤72 chars, imperative mood ("add" not "added"), no trailing period.
- Body only when the why is non-obvious, or for breaking changes / migrations. Wrap body at 72 chars; bullets with `-`.
- Footers: `Closes #123`, `Refs #456`, `BREAKING CHANGE: ...`.
- Breaking change: `feat!:` or `BREAKING CHANGE:` footer.
- Match the project's language and style from `git log --format=%B -5`.

Always include a body for: breaking changes, security fixes, data migrations, or reverts of prior commits.

## Message content

Write the why, not a restatement of the diff. Subject carries the change; body carries non-obvious motive, migration notes, or breaking detail. Scope names the area — omit the filename when scope already covers it. Use emoji only when the project's log already does. Add AI attribution trailers only when the project's own rule requires them.

## Safety

Hard guardrails — pair each with the target behavior:

- Leave git config untouched; create the commit locally for review (no push, no PR offer, no force-push, no hard reset) unless the user explicitly requests that action.
- Run hooks normally; skip (`--no-verify`) only when the user asks.
- Keep secrets out of the index and the commit.
- On failure, fix and create a new commit — amend only when the user explicitly asks and amend rules in the user rules allow it.

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

Atomic split from one dirty tree (illustrative grouping):

```text
# group A — auth fix
fix(auth): validate session before token refresh

# group B — unrelated docs
docs(readme): document session refresh flow
```
