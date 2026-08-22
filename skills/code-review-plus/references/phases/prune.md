# Branch prune — drop old review files

Invoked only by `/code-review-plus prune`. Do not open scope, dispatch, verify, synthesize, persist, fix, perspective, shape, or report files.

## Count first

List timestamped review files in `docs/code-review/` in the **reviewed** repo: `YYYY-MM-DD-HH-MM.md` and collision suffixes (`-2`, `-3`). Exclude `knowns.md`. Sort by filename descending (newest first).

If the directory is missing or the count is **0**: tell the user there is nothing to prune. Stop. Do not ask.

If the count is **≥1**: state the count, the newest stem, and the oldest stem. Then ask. Do not delete yet.

## Ask (only after the count)

Present exactly these choices:

1. Keep the last **3** reviews
2. Keep the last **5** reviews
3. Delete **all** review files
4. Keep the last **N** — the user types a non-negative integer

Use the harness question (ask tool) UI when it exists; otherwise list the four options and wait.

## Apply

Map the answer to **N** (how many newest files to keep):

- Keep 3 → `N=3`
- Keep 5 → `N=5`
- Delete all → `N=0`
- Typed value → that integer. If it is not a non-negative integer, ask again. Do not delete.

Keep the **N** newest files (filename sort). Delete the other timestamped review files only.

If `N ≥ count`: delete nothing. Say so.

`knowns.md` stays. Leave git untouched.

## Report

- Count before
- Stems deleted (or none)
- Count after
- `knowns.md` untouched

## Completion criterion

The count was reported before any prompt. Count 0 stopped without asking. Count ≥1 waited for a choice, then deleted only what that choice requires (or nothing when `N ≥ count`). Summary delivered.
