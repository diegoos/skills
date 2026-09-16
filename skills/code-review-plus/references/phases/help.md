# Branch help — explain the skill

Invoked only by `/code-review-plus help`. This file is the only skill reference for this branch. Emit the Template to the user. Skip review, fix, and prune. No writes.

Translate Template prose to the user's language. Keep command strings, hunter names, paths, and severity labels in English as written.

## Template

```markdown
Code Review Plus reviews a PR or diff for bugs, security, and quality. Invoke it by name. It writes findings under `docs/code-review/` in the **reviewed** repo and does not commit them.

## Commands

| Command | What it does |
| --- | --- |
| `/code-review-plus` | Review this diff (hunters the tier requires) |
| `/code-review-plus help` | This explanation |
| `/code-review-plus <hunter>` | That hunter only: `correctness`, `security`, `architecture`, `quality`, `performance` |
| `/code-review-plus fix` | Apply P0, P1, and vuln; then leftover IDs |
| `/code-review-plus fix all` | Apply every P0–P3 finding (nits included) |
| `/code-review-plus fix 2,3,6` | Apply those Findings IDs (spaces also work) |
| `/code-review-plus prune` | Drop old `docs/code-review/` files (count first) |

`apply` and `implement` are aliases of `fix` (same remainder: empty, `all`, or IDs). Phrases `code quality`, `page performance`, and `only` + a hunter isolate that hunter. Two hunter names without `only` stay a full review. `/code-review-plus security` is this skill's Security hunter.

## Review

The orchestrator sizes the change and picks a tier:

- **trivial** — Correctness + Quality (Security only if the diff touches a sensitive surface)
- **normal** — Correctness, Security, Quality
- **large/sensitive** — those three plus Architecture
- **Performance** — isolated only (`/code-review-plus performance`)

Each hunter hunts one perspective. **silence** is success: a finding needs a proven break, exploit, or quality cost today with `file:line`. A validator (Pass B) keeps or drops candidates. Every kept finding goes in the report. A later run is **delta** when a prior HEAD exists (hunks since that commit; Skip list from knowns and prior Findings).

Quality reads `make-code` when that skill is in the environment; otherwise it uses the built-in Floor and the report says so.

For a deeper security pass, use `/deep-security-review` instead of this skill's Security hunter. Do not run both on the same scope.

## After a review

Mark a false positive or won't-fix in the conversation; that updates `docs/code-review/knowns.md`. Then `/code-review-plus fix` (or `fix all` / `fix <ids>`). `/code-review-plus prune` counts timestamped review files, then asks how many to keep. `knowns.md` stays.
```

## Completion criterion

The Template is the user-facing reply (prose translated when needed; command strings unchanged). No hunters, no persist, no edits in the reviewed repo.
