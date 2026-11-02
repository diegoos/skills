# Branch help — explain the skill

Invoked only by `/code-review-plus help`. This file is the only skill reference for this branch. Emit the Template only.

Translate Template prose to the user's language. Keep command strings, hunter names, paths, and severity labels in English as written.

## Template

````markdown
Code Review Plus reviews a PR or diff for bugs, security, and quality. Invoke it by name. It asks once per session whether to save findings under `docs/code-review/` in the **reviewed** repo or keep them in this session, and never commits them.

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

`apply` and `implement` are aliases of `fix` (same remainder: empty, `all`, or IDs). Phrases `code quality`, `page performance`, and `only` + a hunter isolate that hunter. Two hunter names without `only` stay a full review.

## Review

The orchestrator sizes the change and picks a tier:

- **trivial** — Correctness + Quality (Security only if the diff touches a sensitive surface)
- **normal** — Correctness, Security, Quality
- **large/sensitive** — those three plus Architecture
- **Performance** — isolated only (`/code-review-plus performance`)

Each hunter covers its **floor** (Security follows a method instead) and may add other issues in its scope with today's `file:line`, or a clear issue owned by a hunter that did not run (isolated: only a P0/P1-level break). **Pass B** drops false positives. Every kept finding goes in the report (empty table is valid). A later run is **delta** when a prior HEAD exists, and marks each finding as new or prior.

Quality reads `make-code` when that skill is in the environment; otherwise it uses the built-in Floor and the report says so. <https://github.com/diegoos/skills/tree/main/skills/make-code>

Sibling skills: <https://github.com/diegoos/skills/tree/main/skills>

To install `make-code` skill, you can use `skills` cli:

```bash
npx skills add https://github.com/diegoos/skills --skill make-code
```

## After a review

Mark a false positive or won't-fix in the conversation; that updates `docs/code-review/knowns.md`, or the session memory when you chose not to save. Then `/code-review-plus fix` (or `fix all` / `fix <ids>`). Fix reads `make-code` when that skill is in the environment. `/code-review-plus prune` counts timestamped review files, then asks how many to keep. `knowns.md` stays.

When you chose not to save, the report ends with a Session memory block. Later review and fix calls in this session read it, and nothing is written in the repo.
````

## Completion criterion

The Template is the user-facing reply (prose translated when needed; command strings unchanged). No hunters, no persist, no edits in the reviewed repo.
