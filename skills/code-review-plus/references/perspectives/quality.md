# Pipeline — Quality

If `make-code` is in this environment, READ it once and hunt its Floor (review, no Apply), and return `quality_source: make-code`. Otherwise hunt the default Floor below and return `quality_source: slim-fallback`. **CC** cap is **20** unless the project sets another bar (`./references/complexity.md`).

**KISS** is the path. **DRY** is one representation, earned. **YAGNI** is the stop. **CC** is the local ceiling. **Match** and **Intent over fewest** decide naming and extract.

## Hunt for

- **KISS** — essential path first; a type or file this slice does not call
- **DRY** — second real duplicate; extract with a responsibility name. Copies that mean different things stay copies
- **YAGNI** — provider, flag, or type tree with zero real callers in this diff. Speculative optimization is YAGNI (hot path → Performance)
- **CC** — new or rewritten function above cap **20**, or the project's bar (`eslint complexity`, ruff `C901`, gocyclo). Linear validation, a flat `switch`, and Go `if err != nil` series are not a split trigger. Nesting ≥3 or a happy path a reader cannot state is the readability signal even when CC is at the cap
- **Match** — naming, errors, imports, and function shape from a neighbor of the same kind (or nearest `AGENTS.md` / `CLAUDE.md`). Preference loses
- **Intent over fewest** — intent outranks fewest lines. Keep the helper whose name still carries a concept
- Dead code after a full consumer search (alternate routes, raw envelopes, defensive helpers)
- Docs sync when Phase 1 marked a documentable surface; skip inventing tutorials
- Tests already in the diff: apply `./references/test-quality.md` when that path is in this prompt. Missing tests → Correctness

Layer and module boundary breaks → Architecture. N+1 and demonstrated hot paths → Performance.

## Pass A

`exploit_or_break_path` names today's cost (reader cannot state the happy path, zero callers, unused after consumer search, test that never fails, Match miss, or another quality cost with a pointable line). Configured formatter/linter owns style. Suggested fix preserves error paths. Note `regression_risk` for public names and shared helpers.
