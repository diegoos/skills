# Branch fix — apply findings

Invoked only by `/deep-security-review fix`, `/deep-security-review apply`, or `/deep-security-review implement`. Do not open plan, hunt, verify-and-synthesize, domain, shape, or report template files.

## Resolve targets

1. Load findings from the last security review report in this conversation.
2. If no report exists, ask for the finding list or report; do not invent issues.
3. Default order: P0 → P1 kept vulnerabilities. Apply P2/P3 only when the user asks or lists them.
4. Hardening notes and Verification Gaps are out of scope unless the user explicitly targets them.
5. `needs-runtime` items: defer — do not invent a fix without the missing evidence.

## Apply loop

For each target finding (one at a time, or one atomic cluster that must ship together):

1. Re-read the cited `file:line`, `trace` / `trigger_sketch`, `intended_behavior`, and suggested fix.
2. Apply a **clean minimal local fix** that closes the exploit path. Prefer fail-closed AuthZ and parameterized/allowlisted input. Scope = finding path + callers you must touch; no drive-by refactors outside the finding.
3. Follow **Clean fix** below while editing.
4. Never relax auth, validation, CSRF, or rate limits to make checks pass.
5. Redact secret values in commits, comments, and logs; rotate out-of-band if the finding was a leaked secret. Never echo secret values.
6. Inspect the fix's own diff and re-read touched callers / shared guards.
7. Run project checks when they exist (test / lint / typecheck / format).
8. Run the **fix acceptance gate** before marking the finding closed.

## Clean fix

Close the finding without changing intended secure behavior. Prefer the smallest fail-closed edit that a reader with no PR history can understand.

- **Reuse first** — extend an existing AuthZ helper, schema, allowlist, or encoder before adding a parallel control.
- **One concept per name** — short everyday words; cut prefixes the module already carries; do not invent a second name for the same check.
- **Derivability** — if a value is computable from what is already in scope (session tenant, verified claims), do not pass or store it separately from the request body.
- **Comments** — only state the non-obvious security constraint the code cannot show. Delete narration, conversation/PR history, and comments that restate self-evident code.
- **No unshipped compat** — do not keep old insecure signatures, permissive fallbacks, or shims that only existed earlier in this branch; update callers and delete the dead path.
- **No overfitting** — the diff must stand alone; names and comments must make sense without this conversation.

## Fix acceptance gate

The finding is closed only when all are true:

- The original exploit path no longer holds on reading the code today
- No new demonstrable P0/P1 vulnerability was introduced by this fix
- AuthZ and validation fail closed where the finding required it; intentional design named in the report still holds
- The fix is clean per the section above (reuse, names, no leftover narration/compat)
- Checks that were run passed, or failures are explained and fixed before continuing

If the gate fails: revert or narrow the fix, then retry. Do not proceed to the next finding while a gate failure remains open.

## After all targets

Report:

- Closed findings (ID / severity / domain / file)
- Deferred findings (and why — including needs-runtime)
- Checks run vs not run

Do **not** re-dispatch domain hunters. For a re-review, the user invokes `/deep-security-review` on the **fix diff**, with focus: did each fix close its finding without new P0/P1?

## Completion criterion

Every targeted finding is closed (gate passed) or explicitly deferred. No new demonstrable P0/P1 left by the fixes. Summary of closed vs deferred delivered.
