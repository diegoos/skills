# Refresh

Reconcile existing `docs/` with the current tree. Read the files in the tree. Git history belongs to the update branch. If `docs/` is missing, stop and name **explore** as the next branch.

Language lock: inherit from existing `docs/` (`references/language.md`) unless the user asks to switch.

## Sequence

1. READ `references/phases/survey.md`. Dispatch hunters against the current tree **and** existing docs (voice hunter must read `docs/`).
2. READ `references/phases/confirm.md`. The brief names: files to rewrite, files to keep, files to delete (code no longer earns them), ADRs to keep (default: keep every ADR unless the code contradicts it), language, unknowns.
3. After confirm: rewrite earned files via `references/phases/generate.md`. Delete files confirm marked unearned. Keep an ADR that still holds. Add an ADR only when confirm asked for a new one.
4. READ `references/phases/verify.md`. Stamp `docs/README.md` to today's ISO date.

## Completion criterion

A missing `docs/` ends as the blocked report above. Otherwise survey, confirm, generate, and verify each pass. Existing ADRs remain unless confirm agreed they are contradicted. README lists only files that remain. Stamp is current.
