# Phase 4 — Report template

Fill the Template skeleton below with synthesized findings. The skeleton is the deliverable shape. Only `kept`, adjusted `downgraded`, and carried prior findings appear. When none appear, state that nothing was found **in this pass**, Approve, and leave Findings Overview with header + separator only (no invented data rows).

If the heading order is unclear, READ `./references/examples/report-sample.md`. Do not preload it.

## Render rules

1. **Skeleton fill** — emit Template headings in order. Always emit `## Review Summary`, `### Findings Overview`, and `### Verdict`. Severity detail sections expand findings; they do not replace Findings Overview. Complexity scores stay in the finding body (`parseOrder` CC 14→4), never as an extra Overview column or a separate heading.
2. **Findings Overview is a Markdown pipe table** — seven columns exactly: `ID | Severity | Category | Perspective | File | Issue | Origin`. One data row per kept, downgraded, or carried finding. Origin cells use `new`, `prior <old ID>`, or `prior <old ID>, not re-checked`. Severity cells use 🔴 P0 · 🟠 P1 · 🟡 P2 · ⚪️ P3. Category cells use `🚨 vuln` for vulnerability, else `bug`, `hardening`, or `maintainability`.
3. **Heading strings** — when a section is present, use the Template's English heading text (`## Review Summary`, `### Findings Overview`, `### P0 — Critical (must fix before merge)`, `### P1 — Important (should fix)`, `### P2 — Suggestions (optional improvements)`, `### P3 — Nits (optional)`, `### Dead Code (if any)`, `### Test quality`, `### What Looks Good`, `### Verdict`, `### Session memory`). Translate prose inside sections when the user language differs. Omit the heading when the body would be empty: P0–P3 with no findings at that severity, Dead Code with no verified unused items, `### Test quality` when the review source has no tests or Quality did not run, `### What Looks Good` when there is no specific positive that does not contradict findings, `### Session memory` when `Save: file`.
4. **Pipelines line** — under Review Summary, include `Must NOT change: …`, `Pipelines: … (tier: …)` and `shapes:` when shapes were attached. `Isolated: yes`: `Pipelines: Quality (isolated; tier: normal)`. Isolated Review Summary names the hunter and states the others did not run. Include `Mode: fresh | delta`. When `Prior findings` is not `none`, a line `Prior: carried N · closed since N · new N`. When Quality ran, a line `quality source: make-code | slim-fallback`. Checks: ran … | not run … (one line).
5. **Verdict** — end with one of Approve / Approve with follow-ups / Request changes per the Template rules, plus the fix hint when actionable findings remain. Score per `./references/phases/synthesize.md` § Approval standard. When `quality source` is `slim-fallback`, a line after the apply hint states that `make-code` was not in this environment and Quality used the built-in Floor, plus the make-code Skill links URL. When `Save: session`, `### Session memory` follows with the ledger from `./references/phases/persist.md` § Session ledger.

## Template

```markdown
## Review Summary

[2-3 sentences. Direct assessment: ship it, minor fixes needed, or serious issues. State how many findings were verified vs downgraded/dropped. Isolated: name the hunter; state the others did not run.]

Must NOT change: [concrete APIs, contracts, UX, callers from Phase 1]

Pipelines: [list] ([isolated; ]tier: trivial | normal | large/sensitive)[; shapes: …]

Mode: fresh | delta

[Prior: carried N · closed since N · new N]

quality source: make-code | slim-fallback

Checks: ran … | not run …

### Findings Overview

| ID  | Severity | Category | Perspective | File            | Issue             | Origin |
| --- | -------- | -------- | ----------- | --------------- | ----------------- | ------ |
| 1   | 🔴 P0    | 🚨 vuln  | Security    | path/file.ts:42 | Brief description | new    |

### P0 — Critical (must fix before merge)

**file.ts:42** — What is wrong, why it is exploitable today, data provenance. Include regression_risk for the suggested fix.

[Optional: corrected code block]

### P1 — Important (should fix)

**file.ts:67** — Issue, rationale, regression_risk.

### P2 — Suggestions (optional improvements)

Label hardening items explicitly. List every kept P2.

### P3 — Nits (optional)

List every kept P3.

### Dead Code (if any)

List candidates only after verifying all consumers. Ask: "Should I remove these now-unused items: [list]?"

### Test quality

- Useful: yes | no — [which are not, with file:line]
- Efficient: yes | no — [which are not, with file:line]
- Removable (non-critical): [list] | none. Ask before delete.

### What Looks Good

1-2 specific positives (e.g. stable vocabulary, no unshipped compat stubs, no PR-history comments).

### Verdict

- **Approve** — no verified P0 or P1 and nothing to follow up (isolated: only the hunter that ran; not a full review)
- **Approve with follow-ups** — no verified P0; P2/P3 items, or a verified P1 judged safe to defer (state why), listed by priority
- **Request changes** — at least one **verified** P0, or a verified P1 judged to block this merge (state why)

If Scope set `Oversized: yes`, ask for a split before further review rounds.

To apply: `/code-review-plus fix` (P0, P1, vuln) · `/code-review-plus fix all` · `/code-review-plus fix 2,3` (ids). Aliases: `apply`, `implement`.

[slim-fallback only] make-code was not in this environment; Quality used the built-in Floor. <https://github.com/diegoos/skills/tree/main/skills/make-code>

### Session memory

[Save: session only] Session ledger in a fenced `markdown` block.
```

## Calibration (optional)

If the user asks to calibrate after the report, follow `./references/examples/eval-notes.md` in the conversation. Do not preload it during Phase 4. Do not create that file in the reviewed target repo unless they ask.

## Completion criterion

Phase 4 is done when the skeleton is filled and **not yet sent**: Render rules 1–5 hold, P0–P3 sections list every kept finding at that severity (no hide-cap), Review Summary carries verified-vs-dropped counts, and the apply hint is present when actionable findings remain. Emit only after Phase 4.5.
