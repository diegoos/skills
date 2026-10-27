# Phase 1 — Scope

Establish intent, review source, dispatch tier, `Pipelines`, and stack tags before any pipeline runs.

## Contents

- [Intent questions](#intent-questions)
- [Identify what to review](#identify-what-to-review)
- [Change sizing](#change-sizing)
- [Dispatch tier (checkable)](#dispatch-tier-checkable)
- [Stack tags](#stack-tags)
- [Prior memory](#prior-memory)
- [Tests first](#tests-first)
- [Context summary (required for Phase 2)](#context-summary-required-for-phase-2)
- [Completion criterion](#completion-criterion)

## Intent questions

Answer before dispatching:

```txt
- What is this change trying to accomplish?
- Which specification, task, or PR does it implement?
- What is the expected behavior change?
- What should NOT change?
```

Record `What should NOT change` in concrete terms (APIs, contracts, UX, callers). The **regression gate** (Pass B, synthesize) and the fix **acceptance gate** check fixes against it.

If a PR/commit description exists in context, note whether the first line stands alone as a summary of the change.

## Identify what to review

| Source              | Action                                                       |
| ------------------- | ------------------------------------------------------------ |
| Specific files      | Review those files in full context                           |
| Uncommitted changes | `git diff` (current worktree)                                |
| Feature branch      | `git diff <base>...HEAD` (use repo's default base)           |
| Pasted code         | Review directly                                              |
| Large diff          | Prioritize: new files → modified logic → config → formatting |

No source (empty diff, no named files, no pasted code): say there is nothing to review and stop.

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
| **normal**          | Default feature/bugfix/refactor                                      | Correctness, Security, Quality                                                                              | At most **1** per hunter (priority in Phase 2)                                               |
| **large/sensitive** | ≥~300 logic lines, or touches auth, payments, secrets, raw user HTML | Correctness, Security, Quality, Architecture                                                                | At most **1** per hunter (same priority as `normal`)                                         |

Record `Pipelines` as the hunter names that will run. Isolated (SKILL.md named one hunter): that name, and `Isolated: yes`. Otherwise expand the tier table and set `Isolated: no`. Performance runs only when isolated (`/code-review-plus performance`).

## Stack tags

From paths/extensions and content cues in the review source, record zero or more:

- `ts` (TypeScript/JavaScript/Node), `py` (Python), `go` (Go), `rs` (Rust)
- `llm` when the diff touches prompts, tool/function calling, agent loops, or RAG context assembly

These select optional shapes in Phase 2.

Also note if the diff touches a **documentable surface** (public API, CLI, contract, build/test/release, user-facing behavior) so Quality can check docs sync.

Mark **lockfile in source** when the review source includes `package.json`, a lockfile, or an equivalent manifest.

## Prior memory

The memory is the newest Session ledger in this conversation (`./references/phases/persist.md` § Session ledger). Without one, it is `docs/code-review/` in the reviewed repo.

1. Read knowns: the ledger `## Knowns`, plus `docs/code-review/knowns.md` when present.
2. Read the latest review whose `Branch:` matches the current branch: the newest Session ledger, else the newest timestamped file (`YYYY-MM-DD-HH-MM.md`, not `knowns.md`). Read `## Findings` and `## Fix`.
3. Without git, use that review only when its `Source` names the same files. Otherwise record `Prior review: none`.

From the latest review, build `Prior findings`: each ID with `file:line`, title, and status. IDs under Closed in `## Fix` are `closed`; IDs whose location is in knowns are `known`; every other ID is `open`. `Closed paths` lists the files of the `closed` IDs.

- `Mode: delta` when the latest review recorded a HEAD that is an ancestor of the current HEAD (`git merge-base --is-ancestor <prior HEAD> HEAD`): focus this pass on the hunks since that commit. Otherwise `Mode: fresh`. After a rebase or amend, `Prior findings` still apply.
- `Skip`: knowns and `closed` prior findings, each only while its cited path's behavior is unchanged. `open` prior findings stay off `Skip`; Phase 3 matches or re-checks them.
- A prior isolated `Pipelines` line covers only the hunters it lists.

Record `Knowns`, `Prior review`, `Mode`, `Skip`, `Prior findings`, and `Closed paths` in the context summary (`none` when empty).

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
Pipelines: Correctness, Security, Quality | … (names that will run)
Isolated: yes | no
Mode: fresh | delta
Skip: file:line … | none
Stack tags: ts | py | go | rs | llm | (none)
Documentable surface: yes | no
Lockfile in source: yes | no
Tests in source: yes | no
Tests observed: …
Sizing: small | medium | large
Oversized: yes | no
Knowns: … | none
Prior review: stem / HEAD / none
Save: file | session
Prior findings: ID file:line open | closed | known … | none
Closed paths: file … | none
```

Do not fill `quality_source` here; the Quality hunter returns it.

## Completion criterion

Scope answers written; review source, sizing, oversized, tier, `Pipelines` names, `Isolated`, `Mode`, `Skip`, stack tags, documentable surface, and lockfile-in-source identified; knowns, prior review, `Prior findings`, and `Closed paths` read or recorded as none; context summary ready for Phase 2. Or no source exists, and the run stopped with nothing to review.
