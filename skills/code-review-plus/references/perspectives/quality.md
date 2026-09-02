# Pipeline — Quality

Hunt readability, naming, complexity, dead code, docs sync, tool violations, and (when tests are in the review source) test quality.

When the dispatch prompt lists `test-quality.md`, apply it. Quality hunts tests already in the diff; it does not ask for new tests.

## Hunt for

- Nesting ≥3 levels, nested ternaries, boolean flag parameters in series (`doThing(true, false, true)`), mixed `&&`/`||` soup — the readability signal, even when cyclomatic complexity (CC) is low
- Touched functions with many independent branches: estimate CC as decision points + 1 (`if` / `elif` / loop / `case` / `catch` / `&&` / `||` / `?:`; `else` = 0), or cite the project's complexity tool. Name the move in `suggested_fix` (guard clauses, extract with a responsibility name, lookup/dispatcher, named predicate); a score alone is not a finding
- New or substantially rewritten functions that a reader cannot follow **and** (nesting ≥3 **or** CC ≥11 with no project threshold). One primary signal per `file:line` — nesting, size, or CC, not all three
- One concept → one word in the diff scope; cut prefixes the module/file already carries
- Compound names that spell a full specification instead of the role (only when a shorter name is clear in-file)
- Comments: keep _why_; flag PR/chat history comments and narration of the obvious for removal
- State or parameters derivable from values already in scope; emit here. If the stored value can diverge, `exploit_or_break_path` is that diverge (still this pipeline)
- Names or comments that only make sense with PR/chat history → rewrite in codebase vocabulary
- Clarity finding only when a new reader understands the code faster
- Functions doing too many things (>30 lines is a smell)
- Abstractions before a third real use case. Speculative complexity in this diff with zero real callers (type / strategy / plugin / unshipped provider / unused field, or a `for flexibility` / `in case we need` comment) is YAGNI — emit it. The second real duplicate is not
- Project test, lint, typecheck, format, and complexity rules; if present, run them on touched functions and report violations with `file:line` + score
- Docs sync: when the diff changes a documentable surface (public API, CLI, contract, build/test/release, user-facing behavior), check associated README/refs updated or deleted on deprecation; do not invent "missing tutorial"
- Tests in the diff: apply `test-quality.md` when it is in this prompt (name the break, real SUT, mutation check). Missing tests → Correctness, not this pipeline

## Dead code / redundancy

- Before calling code dead or redundant, confirm **all consumers**, including alternate routes, library-internal fetches, and defensive helpers that handle raw envelopes outside the main helper
- Before calling an abstraction unnecessary, answer why it exists (callers, intent comment, edge cases)
- List candidates and ask; never suggest blind deletion

## Pass A reminders

- Preference (naming/polish) without a codebase inconsistency → do not emit a finding
- Do not suggest inlining, merging unrelated functions, or removing a named abstraction without cost today
- Extract a helper only when the name states a responsibility and a reader is faster today; lowering a complexity score is not a reason
- Linear long function, flat `switch` dispatch, table-driven validation, Go `if err != nil` series, guard clauses / early returns, and a high-CC legacy function the diff barely touched are not complexity candidates
- Style-only prefs without consistency or clarity win are not candidates
- Suggested fix preserves error paths; note `regression_risk` for public names and shared helpers
- `exploit_or_break_path` names today's cost: reader cannot state the happy path, zero callers, or unused after a full consumer search
- Tests in the diff: name the break; do not emit "missing tests" or "skipped TDD"
