# Phase 4 — Report template

Fill the Template skeleton below with synthesized findings. The skeleton is the deliverable shape. Do not send it to the user until Phase 4.5 persist is done. Emit a heading only when that section has content. Only `kept` / adjusted `downgraded` findings appear. Report secrets as `file:line` + type only. When kept count is **0**, state that nothing was found **in this pass**, Approve (or Approve with follow-ups if only hardening remains), and leave Findings Overview with header + separator only (no invented data rows). Isolated: verdict covers this pass only.

If the heading order is unclear, READ `../examples/report-sample.md`. Do not preload it.

## Render rules

1. **Skeleton fill** — emit Template headings in order, only those with a body. Always emit `## Review Summary`, `### Findings Overview`, and `### Verdict`. Severity detail sections expand findings; they do not replace Findings Overview. Complexity scores stay in the finding body (`parseOrder` CC 14→4), never as a seventh Overview column or a separate heading.
2. **Findings Overview is a Markdown pipe table** — six columns exactly: `ID | Severity | Category | Perspective | File | Issue`. One data row per kept/downgraded finding. Severity/category cells use: 🚨 vulnerability · 🔴 P0 · 🟠 P1 · 🟡 P2 · ⚪️ P3. Use 🚨 only when `category` is vulnerability/vuln.
3. **Heading strings** — when a section is present, use the Template's English heading text (`## Review Summary`, `### Findings Overview`, `### P0 — Critical (must fix before merge)`, `### P1 — Important (should fix)`, `### P2 — Suggestions (optional improvements)`, `### P3 — Nits (optional)`, `### Dead Code (if any)`, `### Test quality`, `### What Looks Good`, `### Verdict`). Translate prose inside sections when the user language differs. Omit the heading when the body would be empty: P0–P3 with no findings at that severity, Dead Code with no verified unused items, `### Test quality` when the review source has no tests or Quality did not run, `### What Looks Good` when there is no specific positive that does not contradict findings.
4. **Pipelines line** — under Review Summary, include `Must NOT change: …`, `Pipelines: … (tier: …)` and `shapes:` when shapes were attached. `Isolated: yes`: `Pipelines: Quality (isolated; tier: normal)`. Isolated Review Summary names the hunter and states the others did not run. Include `Mode: fresh | delta`. When Quality ran, a line `quality source: make-code | slim-fallback`. Checks: ran … | not run … (one line).
5. **Verdict** — end with one of Approve / Approve with follow-ups / Request changes per the Template rules, plus the fix hint when actionable findings remain. Score only this pass's findings. Isolated: this pass only. When `quality source` is `slim-fallback`, a line after the apply hint states that `make-code` was not in this environment and Quality used the built-in Floor, plus the make-code Skill links URL. When a deeper security pass is warranted, the **last line** of the user-facing report is the `/deep-security-review` suggestion plus its Skill links URL.

## Template

```markdown
## Review Summary

[2-3 sentences. Direct assessment: ship it, minor fixes needed, or serious issues. State how many findings were verified vs downgraded/dropped. Isolated: name the hunter; state the others did not run.]

Must NOT change: [concrete APIs, contracts, UX, callers from Phase 1]

Pipelines: [list] (isolated; tier: trivial | normal | large/sensitive)[; shapes: …]

Mode: fresh | delta

quality source: make-code | slim-fallback

Checks: ran … | not run …

### Findings Overview

| ID  | Severity | Category | Perspective | File            | Issue             |
| --- | -------- | -------- | ----------- | --------------- | ----------------- |
| 1   | 🔴 P0    | 🚨 vuln  | Security    | path/file.ts:42 | Brief description |

### P0 — Critical (must fix before merge)

Omit this section entirely if none exist.

**file.ts:42** — What is wrong, why it is exploitable today, data provenance. Include regression_risk for the suggested fix.

[Optional: corrected code block]

### P1 — Important (should fix)

Omit this section entirely if none exist.

**file.ts:67** — Issue, rationale, regression_risk.

### P2 — Suggestions (optional improvements)

Omit this section entirely if none exist.

Label hardening items explicitly. List every kept P2.

### P3 — Nits (optional)

Omit this section entirely if none exist.

List every kept P3.

### Dead Code (if any)

Omit this section entirely if none exist.

List candidates only after verifying all consumers. Ask: "Should I remove these now-unused items: [list]?"

### Test quality

Omit this section entirely when the review source has no tests or Quality did not run.

- Useful: yes | no — [which are not, with file:line]
- Efficient: yes | no — [which are not, with file:line]
- Removable (non-critical): [list] | none. Ask before delete.

### What Looks Good

Omit this section entirely when there is no specific positive that does not contradict findings.

1-2 specific positives (e.g. stable vocabulary, no unshipped compat stubs, no PR-history comments).

### Verdict

- **Approve** — no verified P0 in this pass (isolated: this pass only; not a full review)
- **Approve with follow-ups** — no verified P0; hardening/style items listed by priority
- **Request changes** — at least one **verified** P0 exists

If Scope set `Oversized: yes`, ask for a split before further review rounds.

To apply: `/code-review-plus fix` (P0, P1, vuln) · `/code-review-plus fix all` · `/code-review-plus fix 2,3` (ids). Aliases: `apply`, `implement`.

[slim-fallback only] make-code was not in this environment; Quality used the built-in Floor. <https://github.com/diegoos/skills/tree/main/skills/make-code>

[deeper security only, last line] For a deeper security pass: `/deep-security-review` · <https://github.com/diegoos/skills/tree/main/skills/deep-security-review>
```

Omit the `quality source:` line when Quality did not run.

**Deeper security line.** Emit it when this skill's Security hunter ran (or the tier included Security) and the slim pass cannot close the security question for this change: threat model, authz graph, LLM/tool boundary, or supply chain beyond a lockfile glance. Isolated non-Security: omit unless a kept finding is a vulnerability this pass cannot close. Omit the line when the slim pass is enough. Leave `deep-security-review` unstarted. The line includes the Skill links URL.

## Calibration (optional)

If the user asks to calibrate after the report, follow `../examples/eval-notes.md` in the conversation. Do not preload it during Phase 4. Do not create that file in the reviewed target repo unless they ask.

## Completion criterion

Phase 4 is done when the skeleton is filled and **not yet sent**: always-on headings (`## Review Summary`, `### Findings Overview`, `### Verdict`) with English strings; a Findings Overview pipe table with columns `ID | Severity | Category | Perspective | File | Issue` (header + separator always; one data row per kept/downgraded finding, or header-only when kept is 0); P0–P3 sections list every kept finding at that severity (no hide-cap); `Must NOT change` plus pipelines/tier line (`isolated` when `Isolated: yes`; shapes when used); `Mode`; verified-vs-dropped counts in Review Summary (isolated names skipped hunters); `quality source` when Quality ran; slim-fallback line when that source is slim-fallback (includes make-code Skill links URL); deeper-security last line when warranted (includes DSR Skill links URL; omit when the slim pass is enough); optional headings (P0–P3, Dead Code, Test quality, What Looks Good) present only when they have a body. Apply hint included when actionable findings remain. Emit only after Phase 4.5.
