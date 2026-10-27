# Branch fix — apply findings

Invoked only by `/deep-security-review fix` (aliases `apply`, `implement`), with an optional **selection**. This file is the only skill reference for this branch.

## Selection

Parse the remainder after `fix` \| `apply` \| `implement` (case-insensitive). First matching row wins:

| Remainder                         | Selection   | Apply                                                              |
| --------------------------------- | ----------- | ------------------------------------------------------------------ |
| `all`                             | **all**     | Every P0–P3 finding (hardening included). Order P0 → P1 → P2 → P3  |
| integers (`2,3,6` or `2 3 6`)     | **ids**     | Those Findings IDs in given order. Unknown IDs: skip and name them |
| empty (no `all`, no integers)     | **default** | P0 and P1 (vuln). Order P0 → P1                                    |

Inside a severity, keep Findings-table order. Unknown IDs do not stop the rest of **ids**. Verification Gaps stay out of **all** and **default** unless the user listed their Findings ID.

`all` as the first remainder token wins over any IDs that follow.

## Resolve targets

1. Load findings from the last security review report in this conversation.
2. If no report exists, ask for the finding list or report. Leave the list empty until they answer.
3. Restrict the loaded list to the **selection**. Apply only that set.
4. `needs-runtime` items: defer — the missing evidence is still required.

## Make-code

Before the Apply loop: if the make-code skill is available in this environment, READ it once and set **fix source** `make-code`. Else set **fix source** `slim-fallback`.

When **fix source** is `make-code`, each finding uses that skill's workflow on its slice:

- Branch: **write** (vuln, new behavior) · **refactor** (same behavior)
- Trace, Climb, Apply, Prove
- **Must NOT change** and the **fix acceptance gate** still bind
- **CC** on new or rewritten functions: make-code Floor cap (or the project's bar)

When **fix source** is `slim-fallback`, step 3 of the Apply loop is **Clean fix** only.

## Apply loop

For each target finding (one at a time, or one atomic cluster that must ship together):

1. Re-read the cited `file:line`, `trace` / `trigger_sketch`, `intended_behavior`, `regression_risk`, and suggested fix.
2. Apply a **clean minimal local fix** that closes the exploit path and keeps `intended_behavior`. Prefer fail-closed AuthZ and parameterized/allowlisted input. Scope = finding path + callers you must touch.
3. Follow **make-code** Apply when **fix source** is `make-code`; else follow **Clean fix** below.
4. Redact secret values in commits, comments, and logs; rotate out-of-band if the finding was a leaked secret.
5. Auth, validation, CSRF, and rate limits stay fail-closed where the finding required it.
6. Inspect the fix's own diff and re-read touched callers / shared guards.
7. Run project checks when they exist (test / lint / typecheck / format).
8. Run the **fix acceptance gate** before marking the finding closed.

## Clean fix

Close the finding without changing intended secure behavior. Prefer the smallest fail-closed edit that a reader with no PR history can understand.

- **Reuse first** — extend an existing AuthZ helper, schema, allowlist, or encoder before adding a parallel control.
- **One concept per name** — short everyday words; cut prefixes the module already carries; do not invent a second name for the same check.
- **Derivability** — if a value is computable from what is already in scope (session tenant, verified claims), do not pass or store it separately from the request body.
- **Comments** — only state the non-obvious security constraint the code cannot show. Delete narration, conversation/PR history, and comments that restate self-evident code.
- **No unshipped compat** — drop old insecure signatures, permissive fallbacks, or shims that only existed earlier in this branch; update callers and delete the dead path.
- **No overfitting** — the diff must stand alone; names and comments must make sense without this conversation.

## Fix acceptance gate

The finding is closed only when all are true:

- The original exploit path no longer holds on reading the code today
- The original happy path in `intended_behavior` still holds (query result, status codes, non-privileged fields)
- No new demonstrable P0/P1 vulnerability was introduced by this fix
- AuthZ and validation fail closed where the finding required it; **Must NOT change** from the report still holds
- The edit matches make-code Floor when **fix source** is `make-code`; else it matches **Clean fix**
- Checks that were run passed, or failures are explained and fixed before continuing

A test failure from changed behavior is a gate failure (narrow or revert). Auth and validation stay fail-closed when checks go red.

If the gate fails: revert or narrow the fix, then retry. Close the open gate failure before the next finding.

## After all targets

Report to the user:

- Closed findings (ID / severity / domain / file)
- Deferred findings (and why — including needs-runtime)
- Checks run vs not run
- Unknown IDs skipped (when **selection** is **ids**)
- `fix source: make-code | slim-fallback`. When slim-fallback, last line: make-code was not in this environment; fixes used this skill's Clean fix. <https://github.com/diegoos/skills/tree/main/skills/make-code>

When **selection** is **default**, end the user summary with remaining kept findings that were out of this set (still open: not Closed and the break path still holds). Name each leftover ID + severity. Then the two invocations:

```txt
Remaining: 2 (P2), 5 (P3), 6 (P2)
`/deep-security-review fix all`
`/deep-security-review fix 2,5,6`
```

Omit that block when no leftover IDs remain. **all** and **ids** omit it.

Skip domain hunts. For a re-review, the user invokes `/deep-security-review` on the **fix diff**, with focus: did each fix close its finding without new P0/P1?

## Completion criterion

Every finding in the **selection** is closed (gate passed) or explicitly deferred. Unknown IDs named when **ids**. No new demonstrable P0/P1 left by the fixes. Summary of closed vs deferred delivered, including **fix source**. Slim-fallback summary includes the make-code Skill links URL. **default** summary includes leftover IDs plus `fix all` and `fix <ids>` when leftovers exist.
