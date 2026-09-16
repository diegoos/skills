---
name: code-review-plus
description: PR/diff review for bugs, security, and quality; one hunter on demand; fix, fix all, or fix by id; prune or help.
disable-model-invocation: true
metadata:
  version: 0.7.0
  author: "Diego Oliveira"
  tags:
    - code
    - code review
    - security review
    - pr
    - review
---

# Code Review Plus

**Branches:** review (default) → pipelines by tier → validator → synthesize → persist → emit. Fix applies findings with a **regression gate**. Prune drops old `docs/code-review/` files. Help explains the skill.

**Invariants:** One hunter per pipeline. **floor** and **today** live in the Hunt bar (`dispatch.md`). **Pass B** drops false positives; P0/P1 require **proven**. **delta** reads persist. **regression gate** on suggested fixes.

**Reference budget:** Open a phase file when that phase starts. Hunter load: **1** perspective + **0 or 1** shape. Quality bar, shapes, and orchestrator-only paths: `dispatch.md`. Fix reads `make-code` when that skill is in the environment.

## Commands

| Invocation                         | Branch     | Behavior                                                      |
| ---------------------------------- | ---------- | ------------------------------------------------------------- |
| `/code-review-plus`                | **review** | Phases 1→4.5; pipelines by tier                               |
| `/code-review-plus <hunter>`       | **review** | Phases 1→4.5; that hunter only                                |
| `/code-review-plus fix`            | **fix**    | P0, P1, and vuln; then remaining-ID hints                     |
| `/code-review-plus fix all`        | **fix**    | every P0–P3 finding (nits included)                           |
| `/code-review-plus fix <ids>`      | **fix**    | those Findings IDs (`2,3,6` or `2 3 6`)                       |
| `/code-review-plus prune`          | **prune**  | `./references/phases/prune.md` only                           |
| `/code-review-plus help`           | **help**   | how the skill works (`./references/phases/help.md`)           |

Hunter names (case-insensitive): `correctness` \| `security` \| `architecture` \| `quality` \| `performance`. `apply` and `implement` are aliases of `fix` (same **selection** after the token).

Parse the text after `/code-review-plus` (first reserved token wins):

1. `fix` \| `apply` \| `implement` → **fix**; remainder is the **selection** (`all` \| finding IDs \| empty default). Open `fix.md`
2. `prune` → **prune**
3. `help` → **help**. Open `help.md`
4. Two or more hunter names and no `only` → **review**, pipelines by tier
5. A hunter name as the first token → **review**, `Pipelines` = that hunter
6. Else, case-insensitive phrases: `code quality` → Quality; `page performance` → Performance; `only` + a hunter name → that hunter
7. Empty or no match → **review**, pipelines by tier

When the user marks a finding as a false positive or won't-fix, READ `./references/phases/knowns.md`.

## Definition of Done

Done for each phase is the completion criterion in its READ file. Open the next phase file when that criterion is met. Emit the report when Phase 4.5 is done.

### Branch review

| Phase        | Done when                                                                                   | READ                                |
| ------------ | ------------------------------------------------------------------------------------------- | ----------------------------------- |
| 1 Scope      | Intent + source + sizing + tier + Pipelines + Isolated + tags + knowns + context ready      | `./references/phases/scope.md`      |
| 2 Dispatch   | Each Pipelines name returned (empty list valid); shapes recorded when attached              | `./references/phases/dispatch.md`   |
| 2.5 Verify   | Every candidate has status + cited note                                                     | `./references/phases/verify.md`     |
| 3 Synthesize | Surviving findings have required fields + severity and go in the report                     | `./references/phases/synthesize.md` |
| 4 Report     | Skeleton filled (not yet sent)                                                              | `./references/templates/report.md`  |
| 4.5 Persist  | `docs/code-review/<timestamp>.md` written (or read-only gap stated); then emit the skeleton | `./references/phases/persist.md`    |

### Branch fix (`fix` \| `apply` \| `implement`)

| Phase | Done when                                                                                          | READ                         |
| ----- | -------------------------------------------------------------------------------------------------- | ---------------------------- |
| Fix   | Selected findings applied or deferred; `## Fix` filled; default **selection** names leftover IDs   | `./references/phases/fix.md` |

Prerequisite: a review report in this conversation, a `docs/code-review/` memory file, or an explicit finding list. If none exist, ask. Leave the finding list empty until the user provides one.

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

## Skill links

When suggesting `make-code` or `deep-security-review`, include that GitHub URL. Catalog only when naming the collection.

| Skill                  | URL                                                                        |
| ---------------------- | -------------------------------------------------------------------------- |
| make-code              | <https://github.com/diegoos/skills/tree/main/skills/make-code>             |
| deep-security-review   | <https://github.com/diegoos/skills/tree/main/skills/deep-security-review>  |
| catalog                | <https://github.com/diegoos/skills/tree/main/skills>                       |

## Relation to `deep-security-review`

This skill always runs its own Security hunter when Security is in `Pipelines`. Leave `deep-security-review` unstarted. When the slim pass cannot close the security question for this change, the report ends with a `/deep-security-review` suggestion plus its Skill links URL (`report.md`).
