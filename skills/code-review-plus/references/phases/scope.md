# Phase 1 — Scope

Establish intent, review source, dispatch tier, `Pipelines`, and stack tags before any pipeline runs.

## Intent questions

Answer before dispatching:

```txt
- What is this change trying to accomplish?
- Which specification, task, or PR does it implement?
- What is the expected behavior change?
- What should NOT change?
```

Record `What should NOT change` in concrete terms (APIs, contracts, UX, callers). The fix branch uses it as the **regression gate**.

If a PR/commit description exists in context, note whether the first line stands alone as a summary of the change.

## Identify what to review

| Source              | Action                                                       |
| ------------------- | ------------------------------------------------------------ |
| Specific files      | Review those files in full context                           |
| Uncommitted changes | `git diff` (current worktree)                                |
| Feature branch      | `git diff <base>...HEAD` (use repo's default base)           |
| Pasted code         | Review directly                                              |
| Large diff          | Prioritize: new files → modified logic → config → formatting |

## Change sizing

Estimate logic lines changed (ignore pure formatting noise when counting):

| Size   | Rough bar               | Scope note                                                                                        |
| ------ | ----------------------- | ------------------------------------------------------------------------------------------------- |
| Small  | ~100 lines              | Reviewable in one pass                                                                            |
| Medium | ~300 lines              | OK if one logical change                                                                          |
| Large  | ~1000+ or many concerns | Ask for split: stack / horizontal / vertical / by file group; keep refactor separate from feature |

Also watch **file size**: a small diff that grows an already-huge file may need extract-before-add. Set `Oversized: yes` in the context summary (sizing large, or a small diff into a huge file) so Phase 4 can ask for a split.

## Dispatch tier (checkable)

Pick exactly one tier:

| Tier                | When                                                                 | Pipelines                                                                                                   | Shapes                                                                                       |
| ------------------- | -------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| **trivial**         | Docs-only, formatting-only, or rename with no logic                  | Correctness + Quality; add Security only if auth, input boundary, secrets, deps, or security config touched | None                                                                                         |
| **normal**          | Default feature/bugfix/refactor                                      | All five: Correctness, Security, Architecture, Quality, Performance                                         | At most **1** per hunter (priority in Phase 2)                                               |
| **large/sensitive** | ≥~300 logic lines, or touches auth, payments, secrets, raw user HTML | All five                                                                                                    | At most **1** per hunter (same priority as `normal`)                                         |

Record `Pipelines` as the hunter names that will run. Isolated (SKILL.md named one hunter): that name, and `Isolated: yes` (Performance still runs on `trivial`). Otherwise expand the tier table and set `Isolated: no`.

## Stack tags

From paths/extensions and content cues in the review source, record zero or more:

- `web`, `api`
- `ts` (TypeScript/JavaScript/Node), `py` (Python), `go` (Go), `rs` (Rust)
- `llm` when the diff touches prompts, tool/function calling, agent loops, or RAG context assembly

These select optional shapes in Phase 2.

Also note if the diff touches a **documentable surface** (public API, CLI, contract, build/test/release, user-facing behavior) so Quality can check docs sync.

Mark **lockfile in source** when the review source includes `package.json`, a lockfile, or an equivalent manifest.

## Prior memory

If `docs/code-review/` exists in the reviewed repo:

1. Read `docs/code-review/knowns.md` when present.
2. Read the latest timestamped review file (`YYYY-MM-DD-HH-MM.md`, not `knowns.md`).

Skip a known false-positive or won't-fix unless the cited path's behavior changed. When a prior review recorded HEAD, focus this pass on the delta since that commit. A prior `isolated` Pipelines line covers only the hunters it lists.

Record `Knowns` and `Prior review` in the context summary (or `none`).

## Tests first

Tests reveal intent and coverage gaps (missing tests → Correctness signal, not Quality):

- Are there tests for the change?
- Do they test behavior, not implementation details?
- Are edge cases covered?
- Would tests catch a regression?

Mark **tests in source** when the review source includes test paths (`**/*test*`, `**/*.spec.*`, `**/tests/**`, `**/__tests__/**`, `*_test.go`, `*_spec.rb`, and equivalents).

If the repo documents test/lint scripts, the orchestrator may run them readonly and record results; never claim they passed if they did not run.

## Context summary (required for Phase 2)

Compact block for every hunter prompt:

```txt
Intent: …
Must NOT change: …
Source: …
Tier: trivial | normal | large/sensitive
Pipelines: Correctness, Quality | … (names that will run)
Isolated: yes | no
Stack tags: web | api | ts | py | go | rs | llm | (none)
Documentable surface: yes | no
Lockfile in source: yes | no
Tests in source: yes | no
Tests observed: …
Sizing: small | medium | large
Oversized: yes | no
Knowns: … | none
Prior review: stem / HEAD / none
```

## Completion criterion

Scope answers written; review source, sizing, oversized, tier, `Pipelines` names, `Isolated`, stack tags, documentable surface, and lockfile-in-source identified; knowns and prior review read or recorded as none; context summary ready for Phase 2.
