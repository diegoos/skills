# Code Review

Fast, single-pass code review executed by the calling agent — no subagents, no saved reports, and no file edits. Designed for automatic reviews and quick checks right after implementing a feature or fix.

## Usage

User-invoked only (`disable-model-invocation: true`). Call by name:

```text
/code-review                  → uncommitted changes if dirty, else current branch vs base
/code-review 123              → pull request #123 (or full GitHub PR URL)
/code-review abc1234          → specific commit
/code-review main             → current branch compared to main
/code-review src/auth.ts      → specific file(s)
```

## How it works

1. **Resolve scope and context** — resolves the target diff, reads the full modified files (not just hunks), loads repo instructions (`AGENTS.md` / `CLAUDE.md`), and establishes intent and `Must NOT change`.
2. **Single-pass hunt** — reviews the diff across five axes: Correctness, Security, Quality, Architecture, and Performance. For Quality, it reads `make-code` when installed in the environment (`quality source: make-code`), or falls back to a built-in slim Floor (`quality source: slim-fallback`). When the diff touches security, performance, dependencies, or borderline cases, it consults `references/checklists.md` as a lightweight guide.
3. **Self-verify** — re-checks every candidate against callers, middleware, guards, and tests to cut false positives. `P0` and `P1` require proven evidence at a pointable `file:line`.
4. **Emit report** — outputs the same structured report as `code-review-plus` (Summary, 6-column Findings Overview table, P0–P3 sections, Dead Code, What Looks Good, and Verdict), without persistence or fix commands.

## `code-review` vs `code-review-plus`

| Aspect       | `code-review`                                     | `code-review-plus`                                              |
| ------------ | ------------------------------------------------- | --------------------------------------------------------------- |
| Agents       | Single-agent (calling agent)                      | Multi-agent (3–5 parallel hunters + Pass B)                     |
| Cost & speed | Fast and cheap (1 pass)                           | Deep and thorough (multi-phase)                                 |
| Modes        | Review only (read-only)                           | `review`, `<hunter>`, `fix`, `prune`, `help`                    |
| Memory       | Stateless                                         | Saved reports (`docs/code-review/`) or session ledger + `delta` |
| Best for     | Automation, post-feature checks, small/medium PRs | High-risk PRs, security-sensitive changes, iterative fix loops  |
