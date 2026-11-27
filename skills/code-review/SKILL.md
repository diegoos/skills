---
name: code-review
description: Reviews a pull request, diff, commit, or files in one read-only pass for bugs, security, and quality.
disable-model-invocation: true
metadata:
  version: 0.1.0
  author: "Diego Oliveira"
  tags:
    - code review
    - security review
    - pr
    - ci
    - quality
---

# Code Review

Reviews a change in one pass inside the calling agent and emits a structured verdict.

**Hard boundaries:** Run in this agent in one turn (use no subagents). Read-only: leave every repository file untouched and emit the report in the reply only. Write direct, factual prose grounded in cited lines. Report secrets as `file:line` and secret type only, with values redacted.

## Inputs

- `target` (PR URL or number, commit hash, branch name, file paths, or inline code, optional): what to review. When omitted, Step 1 inspects the git worktree and current branch.

## Steps

Work in order. Finish each step when its **Done when** holds.

### 1. Resolve scope and context

Resolve `target`:

| `target`           | Action                                                                                                                                                    |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PR URL or number   | Run `gh pr view <target>` and `gh pr diff <target>`                                                                                                       |
| Commit hash        | Run `git show <hash>`                                                                                                                                     |
| Branch name        | Run `git diff <branch>...HEAD`                                                                                                                            |
| Specific file path | Read those files in full                                                                                                                                  |
| Inline code        | Review the pasted code directly; mark callers and repo instructions `not checked` when no repository is open                                              |
| Omitted            | Check `git status --short`: if dirty, review `git diff`, `git diff --cached`, and untracked files; if clean on a feature branch, `git diff <base>...HEAD` |

Resolve `<base>` from `origin/HEAD`, else `main` or `master`.

**Guards:**

- Empty diff or clean base branch with no `target`: state in one sentence that there is nothing to review and stop.
- `gh` failure: retry a transient error once; on missing `gh`, auth failure, or second error, stop and report what failed, what was skipped, and the next action (authenticate `gh` or pass a local branch or diff).
- Missing git ref, unresolvable `<base>`, or missing file path: stop and report what failed, what was skipped, and the next action.

Once the source is loaded:

- Read each modified file around its changed hunks so surrounding control flow, guards, callers, and error paths are in view.
- Read `AGENTS.md`, `CLAUDE.md`, and `.editorconfig` at the repo root and in modified directories when present.
- Record **Intent** (from PR/commit text and diff; label inferences), **Must NOT change** (concrete APIs, contracts, UX, or callers), **Sizing** (`small` ~100, `medium` ~300, `large` ~1000+ logic lines), and **Oversized** (`yes` when `large` or when the diff materially grows an already-large ~1000-line file, else `no`).
- Run fast readonly project checks (lint/test) only when configured and available; record each under `Checks: ran … | not run …` (if a runtime is missing, record the reason under `not run` and continue).

**Done when:** the review source is loaded (or the run stopped on a guard), every modified file is read around its hunks, applicable repo instruction files are read, and `Intent`, `Must NOT change`, `Sizing`, `Oversized`, and `Checks` are recorded.

### 2. Hunt across five axes

Review the changed code in one pass across all five axes. Flag pre-existing code only when this change makes a broken or vulnerable path reachable.

- **Correctness:** logic errors, off-by-one mistakes, null/undefined access, race conditions, state inconsistencies, swallowed errors or wrong error contracts, unhandled edge cases, and missing tests for non-trivial behavior changes (trivial getters and reexports need none).
- **Security:** follow Context → Compare → Trace. Map existing project controls (auth, session, authz, validation, encoding, query builders), find where the diff skips or weakens them, and trace untrusted input (user, external API, LLM) from entry to sink across privilege boundaries. AuthN alone never proves AuthZ (verify owner or tenant scope).
- **Quality (`make-code` auxiliary):** when the `make-code` skill is available in this environment, read its `## Floor` once (review only) and set `Quality: make-code`. When `make-code` is absent, set `Quality: slim-fallback` and check this slim Floor: **KISS** (simplest working path), **DRY** (extract on second real duplicate), **YAGNI** (single-implementation interfaces, pass-through wrappers, unused options or flags, dead branches), **CC** (cap **20** on new or rewritten functions unless the project sets another bar; nesting ≥3 or an unclear happy path is a readability signal), **Match** (follow neighbor naming, errors, imports, and shape), and **Lean** (reuse in-repo helpers, stdlib, or installed deps instead of re-implementing).
- **Architecture:** broken module boundaries, feature logic placed in shared modules, refactors that relocate complexity without reducing concepts, and fragile type boundaries (`any`, unchecked casts, silent fallbacks). Name a concrete structural move in the fix.
- **Performance:** clear hot-path or production-scale costs visible in the diff today (unbounded work, per-item I/O in loops, missing pagination, blocking sync I/O on request paths, UI render churn, or unsafe caches).

When the diff touches auth, untrusted input sinks, LLM calls, database queries, caching, UI rendering hot paths, or dependency manifests/lockfiles, or when a candidate looks like a borderline false positive, read [`references/checklists.md`](references/checklists.md) for surface cues alongside your own judgment.

**Done when:** every modified file has been checked across all five axes, `references/checklists.md` was read if its condition held, `Quality` (`make-code` or `slim-fallback`) is set, and each candidate records `file:line`, `Perspective`, concrete break/exploit/cost path today, minimal local fix, and `regression_risk` (an empty list is valid).

### 3. Self-verify (high-signal filter)

Re-read callers, middleware, shared guards, and tests for every candidate before keeping it.

- **Drop:** untouched pre-existing issues, style owned by a configured formatter or linter, hypothetical future risks with no cost today, personal preferences with no codebase inconsistency, and dead-code candidates that still have a caller in code, tests, fixtures, config, or dynamic references.
- **Evidence bar:** `P0` and `P1` require **proven** evidence at a pointable `file:line` today. Incomplete paths, runtime-only uncertainty, and defense-in-depth items become `P2` (`hardening`) or drop. Zero findings is a valid result.
- **Category:** `🚨 vuln` (exploitable security issue today), `bug` (reproducible breakage today), `hardening` (defense-in-depth), or `maintainability` (concrete readability, structural, or quality cost today).
- **Severity:**
  - `🔴 P0` — verified critical: exploitable vuln, active bug, data loss, or broken functionality today (blocks merge).
  - `🟠 P1` — important: real bug with lower blast radius, resilience gap, or structural regression today (should fix; defer only with a stated reason).
  - `🟡 P2` — hardening or concrete maintainability/structural improvement (optional follow-up).
  - `⚪️ P3` — nit: small maintainability win with concrete value (optional).
- **Regression gate:** prefer a minimal local fix. Set `regression_risk` to the callers, contracts, tests, or `Must NOT change` items the fix could alter (`none` only after checking). When a real risk exists, state what can break, where (`file:line`), and how to check it.

**Done when:** every candidate from Step 2 has been verified against its callers, middleware, guards, and tests; each kept or downgraded finding has a verified `file:line`, Category, Severity (`P0`/`P1` proven), minimal fix, and `regression_risk`; and verified vs downgraded/dropped counts are recorded.

### 4. Emit report

Emit the template below in order. Keep the English headings; write section prose in the user's language. Format each finding in P0–P3 as `**file:line** — <break, exploit with data provenance, or cost today>. Fix: <minimal local change>. Regression risk: <what can break, where, and how to check, or none>` (label hardening items in P2). Omit empty P0–P3 headings, `### Dead Code (if any)` when no verified unused items exist, and `### What Looks Good` when no specific positive holds without contradicting findings. When zero findings survive, state that nothing was found in this pass, select **Approve**, and keep `### Findings Overview` as header + separator only.

```markdown
## Review Summary

[2-3 sentences: direct ship/fix assessment, plus verified vs downgraded/dropped counts.]

Must NOT change: [concrete APIs, contracts, UX, callers from Step 1]

Run: single-pass · Source: [PR/commit/branch/uncommitted/files/inline] · Sizing: small | medium | large · Quality: make-code | slim-fallback · Checks: ran … | not run …

### Findings Overview

| ID  | Severity | Category | Perspective | File            | Issue             |
| --- | -------- | -------- | ----------- | --------------- | ----------------- |
| 1   | 🔴 P0    | 🚨 vuln  | Security    | path/file.ts:42 | Brief description |

### P0 — Critical (must fix before merge)

### P1 — Important (should fix)

### P2 — Suggestions (optional improvements)

### P3 — Nits (optional)

### Dead Code (if any)

[Verified unused items after full consumer search. Ask: "Should I remove these now-unused items: [list]?"]

### What Looks Good

[1-2 specific positives grounded in the diff.]

### Verdict

- **[Approve | Approve with follow-ups | Request changes]** — [reason per rules: Approve when 0 P0/P1 and 0 follow-ups; Approve with follow-ups when 0 P0 and only P2/P3 or a safely deferrable P1; Request changes when ≥1 verified P0 or merge-blocking P1]

[When Oversized: yes, ask to split the change before further review rounds.]

[When Quality: slim-fallback] make-code was not in this environment; Quality used the built-in Floor. <https://github.com/diegoos/skills/tree/main/skills/make-code>
```

**Done when:** the reply emits `## Review Summary`, `### Findings Overview` (6 columns), every non-empty detail section, and `### Verdict` matching Step 3's counts, with all repository files untouched.
