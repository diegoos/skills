---
name: code-review-plus
description: >-
  Use when the user requests a code review, PR review, diff review, or feedback on changed code and wants independent analysis across correctness, security, architecture, quality, and performance synthesized into a prioritized report. Calibrates severity to avoid false positives, inflated P0s, and findings that contradict project design or global middleware.
metadata:
  version: 0.1.0
  author: "Diego Oliveira"
  tags:
    - code
    - code review
    - security review
    - pr
    - review
---

# Code Review

Review code in **phases**: establish scope, run independent parallel reviews, **verify every finding against the actual code**, synthesize, deliver a prioritized report.

**Core principle:** Each review perspective runs as a separate subagent so findings stay unbiased. Synthesis happens only after all perspectives complete.

**Anti-false-positive principle:** Every finding must be **reproducible by reading the code**. Before writing a finding, open the cited file(s), the immediate caller, and relevant shared utilities (middleware, helpers, config). If you cannot point to the exact line that makes the problem exploitable **today**, it is not a bug — at most, it is hardening or maintainability. Mark it as such.

- **Code Correctness**: logical errors, edge cases, type issues.
- **Code Quality**: readability, naming, duplication, complexity, dead code.
- **Security Reviewer**: input validation, injection risks, data exposure.
- **Architecture Reviewer**: codebase patterns, design consistency, structural alignment.

## Phase 1 — Scope & Context

Before dispatching subagents, answer:

```text
- What is this change trying to accomplish?
- Which specification, task, or PR does it implement?
- What is the expected behavior change?
- What should NOT change?
```

**Identify what to review:**

| Source              | Action                                                       |
| ------------------- | ------------------------------------------------------------ |
| Specific files      | Review those files in full context                           |
| Uncommitted changes | `git diff`                                                   |
| Feature branch      | `git diff <base>...HEAD` (use repo's default base)           |
| Pasted code         | Review directly                                              |
| Large diff          | Prioritize: new files → modified logic → config → formatting |

**Review tests first** — they reveal intent and coverage gaps:

- Are there tests for the change?
- Do they test behavior, not implementation details?
- Are edge cases covered?
- Would tests catch a regression?

## Phase 2 — Parallel Deep Review

Dispatch **five subagents in parallel**. Each subagent receives only its perspective — no shared findings until Phase 3.

### Subagent Prompt Template

Give each subagent:

```text
Review [files/diff] from the [PERSPECTIVE] perspective only.

Context: [1-2 sentences from Phase 1]

Before flagging anything:
- Read the entire cited file, not just the diff snippet.
- Read middleware / modules / utils / project library / global layers before flagging individual routes.
- Trace the full pipeline to the final output, not one step in isolation.
- Read comments explaining intentional design before calling it a bug.
- Verify all consumers before calling code "dead" or "redundant".

Return findings as a list:
- file:line — issue description — category (vulnerability/hardening/maintainability)
- why it is exploitable/breaks today (concrete path, not theory)
- data provenance (for security issues)
- suggested fix (with code if applicable)

Do not review outside your perspective. Do not assign final P0/P1/P2/P3 severity.
```

### Perspectives

#### 1. Correctness & Bugs

- Off-by-one errors, null/undefined access, race conditions, state inconsistencies
- Unhandled error cases, missing return statements, swallowed errors
- Incorrect logic (wrong operator, inverted condition, missing edge case)
- Type mismatches or unsafe coercions
- Does the code match the specification? Are error flows handled?
- Verify framework behavior before asserting (e.g., does this API throw or return `{ data, error }`?)

#### 2. Security

For deeper security analysis, also use `security-review-deep` when available.

- SQL/command/path injection, XSS, CSRF
- Hardcoded secrets, API keys, credentials in code or logs
- Missing input validation or sanitization at system boundaries
- Insecure defaults (permissive CORS, disabled CSRF, weak hashing)
- Authentication/authorization gaps on sensitive operations
- External data (APIs, user input, config) treated as untrusted
- Sensitive data exposure in logs, errors, or responses
- Dependency trust and known vulnerabilities

**Security-specific rules:**

- Check global middleware before flagging a route as "missing CSRF/auth".
- Classify data provenance: direct user input, LLM content, or backend value.
- Evaluate the **final output** of sanitization pipelines, not one step.
- Defense-in-depth gaps are not active vulnerabilities — label them hardening.

#### 3. Architecture

- Are there unbounded loops or unrestricted data fetches?
- Follows existing codebase patterns or justifies new ones
- Clean module boundaries, no circular dependencies
- Business logic in the correct layer (not in controller/view/utility)
- Appropriate abstraction level (no premature or missing abstractions)
- Duplication that should be shared; coupling that should be loosened
- Dependency direction is correct
- Proposed fixes must not break documented intentional design

#### 4. Code Quality & Maintainability

- Descriptive, consistent naming (avoid `temp`, `data`, `result` without context)
- Straightforward control flow (no deep nesting, nested ternaries)
- Functions doing too many things (>30 lines is a smell, not a rule)
- Unnecessary complexity, "clever" tricks
- Abstractions justified by actual reuse (don't generalize before third use case)
- Comments only for non-obvious business logic — not for self-explanatory code
- Determine if the project has a test, lint, type checking, and formatting rules - if so, run them and report any violations.

**Dead code / redundancy rules:**

- Before calling code dead or redundant, confirm **all consumers** — including alternate routes, library-internal fetches, and defensive helpers that handle raw envelopes outside the main helper.
- "Redundant" functions are often small security validations — verify before proposing removal.
- Never suggest blind deletion; list candidates and ask.

#### 5. Performance

For profiling guidance, use `performance-optimization` when available.

- N+1 queries, missing indexes, unbounded loops or data fetches
- Synchronous operations that should be async
- Unnecessary re-renders in UI components
- Missing pagination on list endpoints
- Large object creation in critical paths
- N instances with N listeners is optimization, not a leak, when cleanup exists

## Phase 2.5 — Verify Before Flagging

Apply this checklist to **every** candidate finding before it enters the report. Drop or downgrade any item that fails verification.

```text
- [ ] Did I read the entire cited file (not just the diff snippet)?
- [ ] Did I read middleware / global layer before flagging a route?
- [ ] What is the data provenance (user input / LLM / backend)?
- [ ] Did I trace the full pipeline to the final output?
- [ ] Is there a comment explaining intentional design? Did I respect it?
- [ ] Did I verify framework behavior before asserting failure modes?
- [ ] Did I verify all call paths before calling something dead/redundant?
- [ ] Is my proposed fix consistent with existing logic (no semantic regression)?
- [ ] Can I point to the exact line that makes this exploitable TODAY?
```

### Recurring false positives (do not repeat)

| Pattern                                                                     | Why it is usually wrong                                                                                                                                    |
| --------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `credentials: "include"` leaks cookies cross-origin                         | Browser sends cookies only **for the destination** origin. Relative-path guards are defense-in-depth, not an active vuln.                                  |
| Route "without CSRF" when global middleware covers it                       | Check `middleware.ts` (or equivalent) first. Never praise global CSRF in "What Looks Good" and flag a route below — **self-consistency check**.            |
| XSS in a pipeline that escapes everything and unescapes only fixed literals | If final step escapes `&<>` and `replaceAll` uses only literal strings, attribute/event injection is not possible today. Classify as **future hardening**. |
| Memory leak on listener with cleanup                                        | `onMount` returning cleanup (or `onDestroy`) does not leak. At most P2 optimization.                                                                       |
| Dead/redundant code without checking all consumers                          | Defensive helpers often handle raw fetch envelopes or alternate library paths. Verify before removal.                                                      |
| P0 from "if in the future" or "any evolution could"                         | Future risk is hardening (P2), not a blocker.                                                                                                              |

## Phase 3 — Synthesize Findings

After all subagents complete:

1. **Verify** — run Phase 2.5 checklist on every item; drop or downgrade failures
2. **Deduplicate** — merge overlapping findings from multiple perspectives
3. **Categorize** — assign each finding to exactly one category (table below)
4. **Prioritize** — map category + impact to P0/P1/P2/P3
5. **Self-consistency check** — no contradictions between findings and "What Looks Good"
6. **Identify gaps** — anything no perspective covered? Fill only if clearly warranted and verified
7. **Acknowledge strengths** — note 1-2 specific things done well

### Finding categories (assign before severity)

| Category                         | Definition                                                                      | Typical severity |
| -------------------------------- | ------------------------------------------------------------------------------- | ---------------- |
| **Current vulnerability/bug**    | Exploitable or reproducible breakage **today**, with a pointable line           | P0/P1            |
| **Hardening / defense-in-depth** | Not exploitable today; protects against future evolution or hypothetical caller | P2               |
| **Maintainability / style**      | Fragile, duplicated, inconsistent; no functional impact                         | P2/P3            |

### Severity

| Prefix | Meaning                                                                                     | Author Action                          |
| ------ | ------------------------------------------------------------------------------------------- | -------------------------------------- |
| P0 🔴  | Verified critical — exploitable bug, active vuln, data loss, broken functionality **today** | Must fix before merge                  |
| P1 🟠  | Important — real bugs with lower blast radius, resilience gaps                              | Should fix; defer only with clear plan |
| P2 🟡  | Hardening or minor improvement                                                              | Optional follow-up                     |
| P3 ⚪  | Nit — style or formatting preference                                                        | Can ignore                             |

**Calibration rules:**

- **P0 = blocks merge.** Use only for demonstrated issues, not "could, if someone someday…". If the sentence contains "if in the future" or "any evolution can", **it is not P0**.
- Do not inflate the verdict. Multiple P0s that become 0 upon verification destroys review credibility.
- Legitimate hardening (CSP, HSTS, pagination, `.catch()` on floating promise, defensive `try/finally`) is valuable — present as follow-up, not blocker.
- Not every issue is critical; most are suggestions. A review with 2 real issues beats one with 15 trivial ones.

### Security classification

For each security finding, also classify:

| Level       | Meaning                                                 |
| ----------- | ------------------------------------------------------- |
| CRITICAL 🚨 | Exploitable in production with high impact **today**    |
| HIGH 🟠     | Significant risk with a concrete path, needs prompt fix |
| MEDIUM 🟡   | Defense-in-depth gap, lower immediate risk              |

Include: scenario, impact, data provenance, recommended mitigation.

### Required fields per finding

Each item must include:

1. Exact **file:line**
2. **Category** (vulnerability/bug, hardening, maintainability)
3. **Why it is exploitable/breaks** — concrete path, not theory
4. **Data provenance** when it is a security issue
5. **Severity** per tables above
6. **Proposed fix** that (a) does not break documented design and (b) is consistent with existing logic. If not verified to compile/pass, say so.

## Phase 4 — Deliver Report

```markdown
## Review Summary

[2-3 sentences. Direct assessment: ship it, minor fixes needed, or serious issues. State how many findings were verified vs downgraded/dropped.]

### Findings Overview

| ID  | Severity | Category | Perspective | File            | Issue             |
| --- | -------- | -------- | ----------- | --------------- | ----------------- |
| 1   | P0 🔴    | vuln     | Security    | path/file.ts:42 | Brief description |

### P0 — Critical (must fix before merge)

Omit this section entirely if none exist.

**file.ts:42** — What is wrong, why it is exploitable today, data provenance.

[Optional: corrected code block]

### P1 — Important (should fix)

**file.ts:67** — Issue and rationale.

### P2 — Suggestions (optional improvements)

Keep focused. If more than 5, keep the most impactful. Label hardening items explicitly.

### P3 — Nits (optional)

Max 3. Pick the most impactful only.

### Dead Code (if any)

List candidates only after verifying all consumers. Ask: "Should I remove these now-unused items: [list]?"

### What Looks Good

1-2 specific positives. Not generic praise. Must not contradict findings above.

### Verification

- [ ] Tests pass and cover the change
- [ ] Build succeeds
- [ ] Manual verification done (UI: screenshots if applicable)

State what was **not** verified. "I did not run the build" is better than an unproven "tests pass".

### Verdict

- **Approve** — ready to merge
- **Approve with follow-ups** — no verified P0; hardening/style items listed by priority
- **Request changes** — at least one **verified** P0 exists
```

## Rules

- **File and line context required** — never make the author hunt for issues
- **Explain why**, not just what to change — concrete exploit/break path for P0/P1
- **Show fixes** in fenced code blocks when suggesting corrections
- **Follow existing style** — never suggest changes purely for style if the codebase has an established pattern
- **Respect intentional design** — read comments; fixes must not break documented decisions
- **Calibrate honestly** — P0 only for production-breaking issues demonstrable today
- **No filler** — skip sections with nothing to report
- **Short approval is valid** — "This looks good, ship it" when warranted
- **Ask before deleting** dead code; never recommend blind removal
- **Fail loud on verification** — state unverified claims explicitly

## Example

### Sample output

#### Review Summary

Solid webhook handler implementation. One verified P0 correctness issue before merging. Two hardening items deferred as P2 follow-ups. One initial CSRF concern dropped after verifying global middleware.

#### Findings Overview

| ID  | Severity | Category  | Perspective | File                  | Issue                       |
| --- | -------- | --------- | ----------- | --------------------- | --------------------------- |
| 1   | P0 🔴    | bug       | Correctness | webhook-handler.ts:42 | Unhandled JSON.parse crash  |
| 2   | P2 🟡    | hardening | Performance | webhook-handler.ts:67 | Fixed retry delay           |
| 3   | P2 🟡    | style     | Quality     | webhook-handler.ts:89 | Mixed validation/processing |

#### P0 — Critical

**webhook-handler.ts:42** — Request body passed to `JSON.parse()` without try-catch. Malformed payload crashes the worker. Category: current bug. Provenance: direct user input (HTTP body).

```typescript
let payload;
try {
  payload = JSON.parse(req.body);
} catch {
  return res.status(400).json({ error: "Invalid JSON" });
}
```

#### P2 — Suggestions

**webhook-handler.ts:67** — Fixed 1-second retry delay. Category: hardening. Use exponential backoff to avoid hammering downstream during outages. Not exploitable today.

#### What Looks Good

Idempotency key check at line 35 prevents duplicate processing during retries.

#### Verification

- [ ] Tests pass — not run in this review
- [ ] Build succeeds — not run in this review

#### Verdict

Request changes — one verified P0 before merge. Hardening items are follow-ups.
