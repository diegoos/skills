# Branch fix — apply findings

Invoked only by `/code-review-plus fix` (aliases `apply`, `implement`), with an optional **selection**. Open the memory: the newest Session ledger in this conversation when this session recorded `Save: session`, else `docs/code-review/` in the **reviewed** repo. This file is the only skill reference for this branch.

## Contents

- [Selection](#selection)
- [Resolve targets](#resolve-targets)
- [Make-code](#make-code)
- [Apply loop](#apply-loop)
- [Clean fix](#clean-fix)
- [Fix acceptance gate](#fix-acceptance-gate)
- [After all targets](#after-all-targets)
- [Completion criterion](#completion-criterion)

## Selection

Parse the remainder after `fix` \| `apply` \| `implement` (case-insensitive). First matching row wins:

| Remainder                         | Selection   | Apply                                                              |
| --------------------------------- | ----------- | ------------------------------------------------------------------ |
| `all`                             | **all**     | Every kept P0–P3 finding (nits included). Order P0 → P1 → P2 → P3  |
| integers (`2,3,6` or `2 3 6`)     | **ids**     | Those Findings IDs in given order. Unknown IDs: skip and name them |
| empty (no `all`, no integers)     | **default** | P0, P1, and vuln (🚨). Order P0 → P1 → remaining vuln              |

Dead Code and Test quality "removable" stay ask-before-delete; they are not in **all** or **default** unless the user listed their Findings ID. Inside a severity, keep Findings-table order. Unknown IDs do not stop the rest of **ids**.

`all` as the first remainder token wins over any IDs that follow.

## Resolve targets

1. Load findings from the last review report **in this conversation**, if one exists.
2. Open the memory. `Save: session`: the newest Session ledger in this conversation. Otherwise the file under `docs/code-review/`: this conversation's timestamped file, else the newest `YYYY-MM-DD-HH-MM.md` (not `knowns.md`) whose `Branch:` matches the current branch. Read `## Findings`, `## Details`, `Must NOT change`, and `## Fix` when that heading exists (missing `## Fix` means no apply yet).
3. If step 1 found nothing, use `## Findings` from that memory.
4. If both are empty and the user gave no list, ask. Leave the list empty until they answer.
5. Read `## Fix` when present. Skip an ID listed as Closed when re-reading `file:line` shows the break path is gone. Apply it when the Closed line is stale and the break path still holds. Skip locations in knowns (`knowns.md` or the ledger `## Knowns`).
6. Restrict the loaded list to the **selection**. Apply only that set.

## Make-code

Before the Apply loop: if the make-code skill is available in this environment, READ it once and set **fix source** `make-code`. Else set **fix source** `slim-fallback`.

When **fix source** is `make-code`, each target finding is one make-code request: the `file:line`, the break path, **Must NOT change**, `regression_risk`, and the suggested fix as a hint. make-code runs all its own steps on that slice and picks its branch and its fix. The Apply loop rules and the **fix acceptance gate** still bind. Fold make-code's report for each finding into the fix summary, one line per finding.

When **fix source** is `slim-fallback`, step 2 of the Apply loop uses **Clean fix**.

## Apply loop

For each target finding (one at a time, or one atomic cluster that must ship together):

1. Re-read the cited `file:line`. Take the break path, suggested fix, and `regression_risk` from the report in this conversation, else from `## Details`; derive any that are missing from the re-read. The suggested fix is a hint; the goal is to close the break path.
2. Fix the finding and respect **Must NOT change** from the memory or the report (Review Summary). `make-code`: run it as in **Make-code**. `slim-fallback`: apply a minimal local fix per **Clean fix**. Scope = finding path + callers you must touch + the check make-code adds; no drive-by work outside the finding.
3. Redact secret values in commits, comments, and logs; rotate out-of-band if the finding was a leaked secret.
4. Do not relax auth or validation to make checks pass.
5. Regression check: inspect the fix's own diff, then re-read every caller, contract, and test that `regression_risk` names, plus the callers of each changed symbol. Note each behavior that can still change.
6. Run project checks when they exist (test / lint / typecheck / format). With make-code, its check counts as the test; still run the other checks.
7. Run the **fix acceptance gate** before marking the finding closed.

## Clean fix

Close the finding without changing intended behavior. Prefer the smallest edit that a reader with no PR history can understand.

- **Reuse first.** Use an existing helper/validator/guard in the codebase before inventing a parallel one.
- **One concept per name.** Short everyday words; cut prefixes the module already carries; one name per idea.
- **Derivability.** If a value is computable from what is already in scope, skip a separate pass or store.
- **Comments.** State the non-obvious constraint the code cannot show. Delete narration, conversation/PR history, and comments that restate self-evident code.
- **No unshipped compat.** Drop old signatures, aliases, or shims that only existed earlier in this branch; update callers and delete the dead path.
- **No overfitting.** The diff must stand alone; names and comments must make sense without this conversation.

## Fix acceptance gate

The finding is closed only when all are true:

- The original break/exploit path no longer holds on reading the code today
- No new demonstrable P0/P1 break or vuln was introduced by this fix
- Documented intentional design and named what-must-not-change still hold
- Every caller, contract, and test from the regression check still holds, or the remaining risk is stated
- make-code's criteria hold when **fix source** is `make-code`; else the edit matches **Clean fix**
- Checks that were run pass, or every failure is fixed when this fix caused it and stated when it failed before the fix

If the gate fails: revert or narrow the fix, then retry. After two failed attempts, revert the fix and defer the finding with the reason. Do not proceed to the next finding while a gate failure remains open.

## After all targets

Fill `## Fix` on the memory from Resolve targets: the file, or the Session ledger when `Save: session` (re-emit the whole ledger at the end of the summary). Create the heading after `## Findings` when it is missing. Merge with Closed/Deferred/Open already there (keep prior Closed IDs that still hold). Replace `_(none yet)_` when an older file still has that placeholder. Write one timestamped file per review.

```markdown
## Fix

- Closed: [ID / severity / file] …
- Deferred: [ID + why] … | none
- Open: [ID] … | none
- Risks: [ID: what can break · where] … | none
- Checks: ran … | not run …
- fix source: make-code | slim-fallback
```

Open lists every other kept ID not in Closed or Deferred. The next review re-checks it as a prior finding.

If the memory is missing (read-only gap, no persist, or no ledger), say so in the summary and still report closed vs deferred vs already closed (break path gone, no edit).

Also report to the user, and omit an item that is empty:

- Closed findings (ID / severity / file)
- Already closed, no edit (ID + why the path is gone)
- Deferred findings (and why)
- Regression risks: for each fix that can still change a caller, contract, or test, what can break, where (`file:line`), and how it was checked or how to check it
- Checks run vs not run
- Unknown IDs skipped (when **selection** is **ids**)
- `fix source: make-code | slim-fallback`. When slim-fallback, last line: make-code was not in this environment; fixes used this skill's Clean fix. <https://github.com/diegoos/skills/tree/main/skills/make-code>

When **selection** is **default**, end the user summary with remaining kept findings that were out of this set (not Closed). Name each leftover ID + severity. Then the two invocations:

```txt
Remaining: 2 (P2), 5 (P3), 6 (P2)
`/code-review-plus fix all`
`/code-review-plus fix 2,5,6`
```

Omit that block when no leftover IDs remain. **all** and **ids** omit it.

Skip review pipelines. The next `/code-review-plus` runs as **delta** (`./references/phases/scope.md` § Prior memory).

## Completion criterion

Every finding in the **selection** is closed (gate passed), skipped because the break path is already gone, or explicitly deferred. Unknown IDs named when **ids**. No new demonstrable P0/P1 left by the fixes. Each remaining regression risk is stated with what, where, and how to check. The memory's `## Fix` section (file or Session ledger) is updated with Closed, Deferred, and Open (or the missing-memory gap is stated), including **fix source**. Summary of closed vs skipped vs deferred delivered. Slim-fallback summary includes the make-code Skill links URL. **default** summary includes leftover IDs plus `fix all` and `fix <ids>` when leftovers exist.
