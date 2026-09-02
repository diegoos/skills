---
name: code-review-plus
description: Multi-perspective PR/diff review with a P0–P3 report; one hunter on demand; fix/apply findings or prune saved reviews.
disable-model-invocation: true
metadata:
  version: 0.6.0
  author: "Diego Oliveira"
  tags:
    - code
    - code review
    - security review
    - pr
    - review
---

# Code Review Plus

**Branches:** review (default) → parallel pipelines → double verify → synthesize → report skeleton → persist → emit. Fix branch applies findings with a **regression gate**. Prune drops old `docs/code-review/` files.

**Invariants:** Each pipeline runs as a separate hunter (subagent). Every finding is reproducible from the code. Keep only `proven` or `likely` issues with a pointable line today. Prefer a minimal local fix over a broad refactor.

**Reference budget:** Open a phase file when that phase starts. Each hunter: **1** perspective + **0 or 1** shape. Quality + tests in source: also `./references/test-quality.md`. Orchestrator-only refs stay off hunter prompts (list in dispatch.md).

## Commands

| Invocation                         | Branch     | Behavior                                                      |
| ---------------------------------- | ---------- | ------------------------------------------------------------- |
| `/code-review-plus`                | **review** | Phases 1→4.5; pipelines by tier                               |
| `/code-review-plus <hunter>`       | **review** | Phases 1→4.5; that hunter only                                |
| `/code-review-plus fix`            | **fix**    | `./references/phases/fix.md` only                             |
| `/code-review-plus prune`          | **prune**  | `./references/phases/prune.md` only                           |

Hunter names (case-insensitive): `correctness` \| `security` \| `architecture` \| `quality` \| `performance`. `apply` and `implement` are aliases of `fix`.

Parse the text after `/code-review-plus` (first reserved token wins):

1. `fix` \| `apply` \| `implement` → **fix** (even if the rest names a hunter)
2. `prune` → **prune**
3. Two or more hunter names and no `only` → **review**, pipelines by tier
4. A hunter name as the first token → **review**, `Pipelines` = that hunter
5. Else, case-insensitive phrases: `code quality` → Quality; `page performance` → Performance; `only` + a hunter name → that hunter
6. Empty or no match → **review**, pipelines by tier

`/code-review-plus security` is this skill's Security hunter.

When the user marks a finding as a false positive or won't-fix, READ `./references/phases/knowns.md`.

## Definition of Done

Done for each phase is the completion criterion in its READ file. Open the next phase file when that criterion is met. Emit the report when Phase 4.5 is done.

### Branch review

| Phase        | Done when                                                                                   | READ                                |
| ------------ | ------------------------------------------------------------------------------------------- | ----------------------------------- |
| 1 Scope      | Intent + source + sizing + tier + Pipelines + Isolated + tags + knowns + context ready      | `./references/phases/scope.md`      |
| 2 Dispatch   | Each Pipelines name returned candidates; shapes recorded when attached                      | `./references/phases/dispatch.md`   |
| 2.5 Verify   | Every candidate has status + cited note; P0 verifier ran or skipped                         | `./references/phases/verify.md`     |
| 3 Synthesize | Surviving findings have required fields + severity                                          | `./references/phases/synthesize.md` |
| 4 Report     | Skeleton filled (not yet sent)                                                              | `./references/templates/report.md`  |
| 4.5 Persist  | `docs/code-review/<timestamp>.md` written (or read-only gap stated); then emit the skeleton | `./references/phases/persist.md`    |

### Branch fix (`fix` \| `apply` \| `implement`)

| Phase | Done when                                                                                          | READ                         |
| ----- | -------------------------------------------------------------------------------------------------- | ---------------------------- |
| Fix   | Findings applied or deferred without new demonstrable P0/P1; this review's `## Fix` section filled | `./references/phases/fix.md` |

Prerequisite: a review report in this conversation, a `docs/code-review/` memory file, or an explicit finding list. If none exist, ask. Leave the finding list empty until the user provides one.

### Branch prune

| Phase | Done when                                                                                          | READ                           |
| ----- | -------------------------------------------------------------------------------------------------- | ------------------------------ |
| Prune | Count first; then delete per keep-3 / keep-5 / all / N                                             | `./references/phases/prune.md` |

## Rules

- Report secrets as `file:line` + type only; redact values in the report and in fixes

## Relation to `deep-security-review`

Both skills are user-invoked. Use this skill for multi-perspective PR/diff review (optional stack shapes, including `llm`), including `/code-review-plus security`. Hint `/deep-security-review` as a deeper pass.
