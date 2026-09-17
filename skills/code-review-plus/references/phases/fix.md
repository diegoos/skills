# Branch fix — apply findings

Invoked only by `/code-review-plus fix` (aliases `apply`, `implement`), with an optional **selection**. Open `docs/code-review/` in the **reviewed** repo. This file is the only skill reference for this branch.

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
2. Open the matching memory file under `docs/code-review/` (this conversation's timestamped file, else the newest `YYYY-MM-DD-HH-MM.md`, not `knowns.md`). Read `## Findings`, `Must NOT change`, and `## Fix` when that heading exists (missing `## Fix` means no apply yet).
3. If step 1 found nothing, use `## Findings` from that memory file.
4. If both are empty and the user gave no list, ask. Leave the list empty until they answer.
5. Read `## Fix` when present. Skip an ID listed as Closed when re-reading `file:line` shows the break path is gone. Apply it when the Closed line is stale and the break path still holds. Skip locations in `knowns.md`.
6. Restrict the loaded list to the **selection**. Apply only that set.

## Make-code

Before the Apply loop: if the make-code skill is available in this environment, READ it once and set **fix source** `make-code`. Else set **fix source** `slim-fallback`.

When **fix source** is `make-code`, each finding uses that skill's workflow on its slice:

- Branch: **write** (bug, vuln, new behavior) · **refactor** (same behavior) · **improve** only when the finding is Performance with a named hotspot
- Trace, Climb, Apply, Prove
- **Must NOT change** and the **fix acceptance gate** still bind
- **CC** on new or rewritten functions: make-code Floor cap (or the project's bar)

When **fix source** is `slim-fallback`, step 3 of the Apply loop is **Clean fix** only.

## Apply loop

For each target finding (one at a time, or one atomic cluster that must ship together):

1. Re-read the cited `file:line` and the finding's `regression_risk` / suggested fix.
2. Apply a **clean minimal local fix** that closes the issue and respects **Must NOT change** from the memory file or the report (Review Summary). Scope = finding path + callers you must touch; no drive-by work outside the finding.
3. Follow **make-code** Apply when **fix source** is `make-code`; else follow **Clean fix** below.
4. Redact secret values in commits, comments, and logs; rotate out-of-band if the finding was a leaked secret.
5. Do not relax auth or validation to make checks pass.
6. Inspect the fix's own diff and re-read touched callers.
7. Run project checks when they exist (test / lint / typecheck / format).
8. Run the **fix acceptance gate** before marking the finding closed.

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
- The edit matches make-code Floor when **fix source** is `make-code`; else it matches **Clean fix**
- Checks that were run passed, or failures are explained and fixed before continuing

If the gate fails: revert or narrow the fix, then retry. Do not proceed to the next finding while a gate failure remains open.

## After all targets

Fill `## Fix` on the memory file from Resolve targets. Create the heading after `## Findings` when it is missing. Merge with Closed/Deferred already there (keep prior Closed IDs that still hold). Replace `_(none yet)_` when an older file still has that placeholder. Write one timestamped file per review.

```markdown
## Fix

- Closed: [ID / severity / file] …
- Deferred: [ID + why] … | none
- Checks: ran … | not run …
- fix source: make-code | slim-fallback
```

If that file is missing (read-only gap or no persist), say so in the summary and still report closed vs deferred vs already closed (break path gone, no edit).

Also report to the user:

- Closed findings (ID / severity / file)
- Already closed, no edit (ID + why the path is gone)
- Deferred findings (and why)
- Checks run vs not run
- Unknown IDs skipped (when **selection** is **ids**)
- `fix source: make-code | slim-fallback`. When slim-fallback, last line: make-code was not in this environment; fixes used this skill's Clean fix. <https://github.com/diegoos/skills/tree/main/skills/make-code>

When **selection** is **default**, end the user summary with remaining kept findings that were out of this set (still open: not Closed and the break path still holds). Name each leftover ID + severity. Then the two invocations:

```txt
Remaining: 2 (P2), 5 (P3), 6 (P2)
`/code-review-plus fix all`
`/code-review-plus fix 2,5,6`
```

Omit that block when no leftover IDs remain. **all** and **ids** omit it.

Skip review pipelines. The next `/code-review-plus` is **delta**: closed paths plus new P0/P1 on the fix hunks. Do not re-dispatch the full hunter set.

## Completion criterion

Every finding in the **selection** is closed (gate passed), skipped because the break path is already gone, or explicitly deferred. Unknown IDs named when **ids**. No new demonstrable P0/P1 left by the fixes. The memory file's `## Fix` section is updated (or the missing-file gap is stated), including **fix source**. Summary of closed vs skipped vs deferred delivered. Slim-fallback summary includes the make-code Skill links URL. **default** summary includes leftover IDs plus `fix all` and `fix <ids>` when leftovers exist.
