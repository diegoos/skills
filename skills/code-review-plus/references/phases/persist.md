# Phase 4.5 — Persist

Orchestrator-only. Open after the Phase 4 skeleton exists. `Save: file` writes memory in the **reviewed** repo. `Save: session` fills the Session ledger and writes nothing in the repo. Then emit the report.

## Write the review file first

Applies to `Save: file`. Create `docs/code-review/` (and `docs/` if needed). Leave git untouched.

Filename: `docs/code-review/YYYY-MM-DD-HH-MM.md` (local time, 24h). If that path exists, append `-2` (then `-3`). H1 is the file stem.

The `Pipelines` line matches the report: `Isolated: yes` gets `(isolated; tier: …)`; `Isolated: no` lists the hunters that ran.

Fill this skeleton. Emit a heading only when that section has content. Always write the metadata block, `## Findings`, `## Details`, and `## Notes`. Add `## Test quality` only when the review source includes tests and Quality ran. Omit `## Fix` until the `/code-review-plus fix` branch runs.

```markdown
# YYYY-MM-DD-HH-MM

Source: …
Tier: trivial | normal | large/sensitive
Mode: fresh | delta
HEAD: …
Branch: …
Must NOT change: …

Pipelines: … ([isolated; ]tier: …)[; shapes: …]

## Findings

| ID  | Severity | Category | Perspective | File | Issue | Origin |
| --- | -------- | -------- | ----------- | ---- | ----- | ------ |

## Details

- 1 — break: … · fix: … · regression_risk: …

## Test quality

- Useful: …
- Efficient: …
- Removable (non-critical): … (list and ask; do not delete)

## Notes

Verified: … / dropped: … / downgraded: …
Prior: carried … / closed since … / new …
quality source: make-code | slim-fallback
serial: yes | (omit line when parallel or one hunter)
Checks: ran … | not run …
```

Findings rows match the report table (kept, adjusted downgraded, and carried). Header + separator only when none appear. `## Details` holds one line per ID, so a later fix runs without this conversation.

Omit the `quality source:` line when Quality did not run. Omit `serial:` when hunters ran in parallel or only one hunter ran. Omit `Prior:` when `Prior findings` is `none`.

If the **reviewed repo** is read-only, record the gap under Notes and still emit the report. Write the file or state that gap.

## Session ledger

Applies to `Save: session`. Fill the same skeleton in the conversation instead of a file, with three changes: the H1 is `# Session ledger YYYY-MM-DD-HH-MM`, `## Details` is omitted (the report in this conversation carries them), and `## Knowns` (columns from `./references/phases/knowns.md`) holds the rows the user dismissed in this session. Put the ledger at the end of the reply under `### Session memory`, in a fenced `markdown` block. A later fix or knowns update re-emits the whole ledger, so the newest ledger in the conversation is the memory. Leave the reviewed repo untouched.

## Then emit

Phase 4.5 is done when the file exists, the ledger is filled, or the read-only gap is stated. Only then send the Phase 4 skeleton as the user-facing reply.

## Completion criterion

`Save: file`: the timestamped review file is written with Findings, Details, Notes, and Mode (Test quality only when tests are in source and Quality ran; `quality source` when Quality ran; `## Fix` only after the first apply), or the read-only gap is stated. `Save: session`: the Session ledger holds the same Findings and Notes, and the reviewed repo is untouched. The report is ready to emit.
