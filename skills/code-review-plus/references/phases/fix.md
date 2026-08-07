# Branch fix — apply findings

Invoked only by `/code-review-plus fix`, `/code-review-plus apply`, or `/code-review-plus implement`. Do not open scope, dispatch, verify, synthesize, perspective, or report template files.

## Resolve targets

1. Load findings from the last review report in this conversation.
2. If no report exists, ask for the finding list or report — do not invent issues.
3. Default order: P0 → P1. Apply P2/P3 only when the user asks or lists them.

## Apply loop

For each target finding (one at a time, or one atomic cluster that must ship together):

1. Re-read the cited `file:line` and the finding's `regression_risk` / suggested fix.
2. Apply the **minimal local fix** that closes the issue and respects Phase 1 what-must-not-change (from the report context).
3. Inspect the fix's own diff and re-read touched callers.
4. Run project checks when they exist (test / lint / typecheck / format).
5. Run the **fix acceptance gate** before marking the finding closed.

## Fix acceptance gate

The finding is closed only when all are true:

- The original break/exploit path no longer holds on reading the code **today**
- No new demonstrable P0/P1 break or vuln was introduced by this fix
- Documented intentional design and named what-must-not-change still hold
- Checks that were run passed, or failures are explained and fixed before continuing

If the gate fails: revert or narrow the fix, then retry. Do not proceed to the next finding while a gate failure remains open.

## After all targets

Report:

- Closed findings (ID / severity / file)
- Deferred findings (and why)
- Checks run vs not run

Do **not** re-dispatch the five pipelines. For a re-review, the user invokes `/code-review-plus` on the **fix diff**, with focus: did each fix close its finding without new P0/P1?

## Completion criterion

Every targeted finding is closed (gate passed) or explicitly deferred. No new demonstrable P0/P1 left by the fixes. Summary of closed vs deferred delivered.
