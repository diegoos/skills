# Pipeline — Quality

Hunt readability, naming, complexity, dead code, docs sync, tool violations, and (when tests are in the review source) test quality.

For named structural moves, see `../remedies.md`.
If the review source includes test paths, also READ `../test-quality.md`. Quality hunts tests already in the diff; it does not ask for new tests.

## Hunt for

- Nesting ≥3 levels, nested ternaries, boolean flag parameters in series (`doThing(true, false, true)`)
- One concept → one word in the diff scope; cut prefixes the module/file already carries
- Compound names that spell a full specification instead of the role (only when a shorter name is clear in-file)
- Comments: keep _why_; flag PR/chat history comments and narration of the obvious for removal
- State or parameters derivable from values already in scope; if the stored value can diverge → Correctness signal
- Names or comments that only make sense with PR/chat history → rewrite in codebase vocabulary
- Clarity finding only when a new reader understands the code faster
- Functions doing too many things (>30 lines is a smell)
- Abstractions before a third real use case
- Project test, lint, typecheck, and format rules; if present, run them and report violations
- Docs sync: when the diff changes a documentable surface (public API, CLI, contract, build/test/release, user-facing behavior), check associated README/refs updated or deleted on deprecation; do not invent "missing tutorial"
- Tests in the diff: apply `../test-quality.md` (name the break, real SUT, mutation check). Missing tests → Correctness, not this pipeline

## Dead code / redundancy

- Before calling code dead or redundant, confirm **all consumers**, including alternate routes, library-internal fetches, and defensive helpers that handle raw envelopes outside the main helper
- Before calling an abstraction unnecessary, answer why it exists (callers, intent comment, edge cases)
- List candidates and ask; never suggest blind deletion

## Pass A reminders

- Preference (naming/polish) without a codebase inconsistency → do not emit a finding
- Do not suggest inlining, merging unrelated functions, or removing a named abstraction without cost today
- Style-only prefs without consistency or clarity win are not candidates
- Suggested fix preserves error paths; note `regression_risk` for public names and shared helpers
- Tests in the diff: name the break; do not emit "missing tests" or "skipped TDD"
