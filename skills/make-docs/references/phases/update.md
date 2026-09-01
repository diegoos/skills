# Update

Sync existing `docs/` with commits since the last stamp. Incremental patch. Do not rewrite the suite. Language lock: inherit from existing `docs/` (`./references/language.md`).

## Scope

Read `docs/README.md` for `> Updated on <ISO-date>`. Count commits since that date (`git rev-list --count HEAD --since=<date>`).

- Missing stamp: ask for the range, or offer **refresh**. Wait.
- Count ≤ 10: cover all commits since the stamp. Orchestrator diffs; skip hunters.
- Count > 10: inform the count and ask: cover all, last N commits, or a specific base (SHA / date). Wait before diffing. If the user covers all, dispatch 1–3 hunters from `./references/phases/survey.md` scoped to changed paths.

**Done when:** base revision chosen (all since stamp, last N, or user-specified base).

## Diff

`git diff <base>..HEAD` plus unstaged/uncommitted changes. Classify each changed path: structural → architecture, behavioral → specs, decision → ADR.

Ambiguous classification (pure refactor vs behavior): ask. Do not record "no spec change" until the user agrees or the diff is clearly non-behavioral.

**Done when:** every changed path is classified, or the user answered the ambiguous ones.

## Patch

Load the matching template before editing a file. Apply the classified changes only. Pure refactor: record "no spec change" in chat. Set `> Updated on` in `docs/README.md` to today's ISO date.

**Done when:** every classified change is reflected or waived in chat; stamp refreshed.

## Verify

READ `./references/phases/verify.md`.

## Completion criterion

Scope, diff, and patch criteria above hold, and verify passes.
