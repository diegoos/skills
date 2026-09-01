# Phase 4.5 — Persist

Orchestrator-only. Open after the Phase 4 skeleton exists. Write memory in the **reviewed** repo, then emit the report.

## Write the review file first

Create `docs/code-review/` (and `docs/` if needed). Leave git untouched.

Filename: `docs/code-review/YYYY-MM-DD-HH-MM.md` (local time, 24h). If that path exists, append `-2` (then `-3`). H1 is the file stem.

The `Pipelines` line matches the report: `Isolated: yes` gets `(isolated; tier: …)`; `Isolated: no` lists the hunters that ran.

Fill this skeleton. Emit a heading only when that section has content. Always write the metadata block, `## Findings`, and `## Notes`. Add `## Test quality` only when the review source includes tests and Quality ran. Omit `## Fix` until the `/code-review-plus fix` branch runs.

```markdown
# YYYY-MM-DD-HH-MM

Source: …
Tier: trivial | normal | large/sensitive
HEAD: …
Branch: …
Must NOT change: …

Pipelines: … (isolated; tier: …)[; shapes: …]

## Findings

| ID  | Severity | Category | Perspective | File | Issue |
| --- | -------- | -------- | ----------- | ---- | ----- |

## Test quality

- Useful: …
- Efficient: …
- Removable (non-critical): … (list and ask; do not delete)

## Notes

Verified: … / dropped: … / downgraded: …
P0 verifier: ran | skipped (reason: …)
serial: yes | (omit line when parallel or one hunter)
```

Findings rows match the report table (kept / adjusted downgraded only). Header + separator only when kept is 0.

If the **reviewed repo** is read-only, record the gap under Verification and still emit the report. Write the file or state that gap.

## Then emit

Phase 4.5 is done when the file exists (or the read-only gap is stated). Only then send the Phase 4 skeleton as the user-facing reply.

## Fix branch

The fix branch loads Findings from this conversation or from `docs/code-review/`, then reads `## Fix` to skip work already done. Instructions live in the fix branch (`/code-review-plus fix`). Write one timestamped file per review.

To drop old timestamped files: `/code-review-plus prune`.

## Completion criterion

The timestamped review file is written with Findings and Notes (Test quality only when tests are in source and Quality ran; `## Fix` only after the first apply), or the read-only gap is stated. The report is ready to emit.
