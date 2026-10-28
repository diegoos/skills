---
name: code-review-plus
description: Reviews a PR or diff for bugs, security, and quality, and applies selected findings.
disable-model-invocation: true
metadata:
  version: 0.7.1
  author: "Diego Oliveira"
  tags:
    - code review
    - security review
    - pr
    - review
---

# Code Review Plus

**Branches:** review (default) → save choice → pipelines by tier → verify (Pass B) → synthesize → report → persist → emit. Fix applies findings with an **acceptance gate**. Prune drops old `docs/code-review/` files. Help explains the skill.

**Invariants:** One hunter per pipeline. **floor** and **today** live in the Hunt bar (`./references/phases/dispatch.md`). **Pass B** drops false positives; P0/P1 require **proven**. **delta** when a prior review recorded HEAD. **regression gate** on suggested and applied fixes. **Save** (file or session) is asked once per session.

**Terms:** a hunter reviews one perspective. The `pipeline` field and the report's `Perspective` column name the hunter.

**Reference budget:** Open a phase file when that phase starts. Hunter load: **1** perspective + **0 or 1** shape. Quality bar, shapes, and orchestrator-only paths: `./references/phases/dispatch.md`. Fix reads `make-code` when that skill is in the environment. Paths in references resolve from the skill folder.

## Commands

| Invocation                         | Branch     | Behavior                                                      |
| ---------------------------------- | ---------- | ------------------------------------------------------------- |
| `/code-review-plus`                | **review** | Phases 0→4.5; pipelines by tier                               |
| `/code-review-plus <hunter>`       | **review** | Phases 0→4.5; that hunter only                                |
| `/code-review-plus fix`            | **fix**    | P0, P1, and vuln; then remaining-ID hints                     |
| `/code-review-plus fix all`        | **fix**    | every P0–P3 finding (nits included)                           |
| `/code-review-plus fix <ids>`      | **fix**    | those Findings IDs (`2,3,6` or `2 3 6`)                       |
| `/code-review-plus prune`          | **prune**  | `./references/phases/prune.md` only                           |
| `/code-review-plus help`           | **help**   | how the skill works (`./references/phases/help.md`)           |

Hunter names (case-insensitive): `correctness` \| `security` \| `architecture` \| `quality` \| `performance`. `apply` and `implement` are aliases of `fix` (same **selection** after the token).

Parse the text after `/code-review-plus` (first reserved token wins):

1. `fix` \| `apply` \| `implement` → **fix**; remainder is the **selection** (`all` \| finding IDs \| empty default). Open `./references/phases/fix.md`
2. `prune` → **prune**
3. `help` → **help**. Open `./references/phases/help.md`
4. Two or more hunter names and no `only` → **review**, pipelines by tier
5. A hunter name as the first token → **review**, `Pipelines` = that hunter
6. Else, case-insensitive phrases: `code quality` → Quality; `page performance` → Performance; `only` + a hunter name → that hunter
7. Empty or no match → **review**, pipelines by tier

When the user marks a finding as a false positive or won't-fix, READ `./references/phases/knowns.md`.

## Definition of Done

Done for each phase is the completion criterion in its READ file. Open the next phase file when that criterion is met.

### Branch review

| Phase        | Done when                                                                                   | READ                                |
| ------------ | ------------------------------------------------------------------------------------------- | ----------------------------------- |
| 0 Save       | `Save` recorded as file or session; asked once per session                                  | `./references/phases/save.md`       |
| 1 Scope      | Intent + source + sizing + tier + Pipelines + Isolated + tags + knowns + context ready      | `./references/phases/scope.md`      |
| 2 Dispatch   | Each Pipelines name returned (empty list valid); shapes recorded when attached              | `./references/phases/dispatch.md`   |
| 2.5 Verify   | Every candidate has status + cited note                                                     | `./references/phases/verify.md`     |
| 3 Synthesize | Surviving findings have required fields + severity and go in the report                     | `./references/phases/synthesize.md` |
| 4 Report     | Skeleton filled (not yet sent)                                                              | `./references/templates/report.md`  |
| 4.5 Persist  | File written, session ledger filled, or read-only gap stated; then emit the skeleton        | `./references/phases/persist.md`    |

### Branch fix (`fix` \| `apply` \| `implement`)

| Phase | Done when                                                                                          | READ                         |
| ----- | -------------------------------------------------------------------------------------------------- | ---------------------------- |
| Fix   | Selected findings applied or deferred; `## Fix` filled; default **selection** names leftover IDs   | `./references/phases/fix.md` |

### Branch prune

| Phase | Done when                                                                                          | READ                           |
| ----- | -------------------------------------------------------------------------------------------------- | ------------------------------ |
| Prune | Count first; then delete per keep-3 / keep-5 / all / N                                             | `./references/phases/prune.md` |

### Branch help

| Phase | Done when                                                                                          | READ                          |
| ----- | -------------------------------------------------------------------------------------------------- | ----------------------------- |
| Help  | User-facing explanation emitted; no review, fix, prune, or writes                                  | `./references/phases/help.md` |

## Rules

- Report secrets as `file:line` + type only; redact values in the report and in fixes
- Write short and direct unless the user asks for detail. A finding still gives a fix run what it needs: `file:line`, the break path, the fix direction, and `regression_risk`. A real regression risk is the exception: explain what can break, where, and how to check it
- When the conversation is compacted, keep a short findings history in the summary: the `Save` choice and, for the newest review, each finding's ID, severity, `file:line`, and status (open, closed, deferred, or known). With `Save: session`, keep the newest Session ledger verbatim; it is the only memory

## Skill links

When suggesting `make-code`, include that GitHub URL. Catalog only when naming the collection.

| Skill                  | URL                                                                        |
| ---------------------- | -------------------------------------------------------------------------- |
| make-code              | <https://github.com/diegoos/skills/tree/main/skills/make-code>             |
| catalog                | <https://github.com/diegoos/skills/tree/main/skills>                       |
