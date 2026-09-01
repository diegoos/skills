# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Every skill has `agents/openai.yaml` for ChatGPT and Codex (picker name, short blurb, default `$skill` prompt). Skills with `disable-model-invocation` set `allow_implicit_invocation: false`.
- `make-docs`: `/make-docs refresh` re-surveys the current tree against existing `docs/`; ADRs stay unless the code contradicts them; confirm before any write; up to three read-only hunters (structure, behavior, voice) with serial fallback; language lock; docs anti-slop; `metadata.version` → `0.2.0`.
- `code-review-plus`: `/code-review-plus prune` counts timestamped files under `docs/code-review/` first, then asks whether to keep the last 3, the last 5, delete all, or keep a typed N; never deletes `knowns.md`.
- `code-review-plus`: persist each review under `docs/code-review/` in the reviewed repo (`YYYY-MM-DD-HH-MM.md` with Findings and `## Fix`); `knowns.md` when the user marks a false positive or won't-fix; Scope reads knowns and the latest review; `metadata.version` → `0.5.0`.
- `code-review-plus`: Quality `test-quality.md` when tests are in the diff (name-the-break, real SUT, mutation check, AI-slop / utility questions); `### Test quality` on the report.
- `code-review-plus`: human `README.md` with commands, memory layout, and a mermaid flow of review vs fix.
- `frontend-design-plus`: skill for building, restyling, or polishing web UI (HTML/CSS). README says when it runs (create a page, improve a layout, restyle, polish) and why occupancy in DESIGN.md plus Fail-ifs come before a second look. The run is Classify, Origin, Layout, markup from DESIGN.md, Floor, then Critique. DESIGN.md holds Job, objects, Claim, Pair, Signature, and the enter ASCII. After markup, [critique.md](skills/frontend-design-plus/reference/critique.md) checks that spine; [anti-slop.md](skills/frontend-design-plus/reference/anti-slop.md) holds the design and copy Fail-ifs. If the harness has a browser tool, Walk covers 1440 and 375.
- `markdown-writer`: human `README.md` with the CommonMark 0.31.2, GFM, and markdownlint Rules URLs used to write the skill.

### Changed

- `write-great-instructions`: now a writing guide only; dropped bootstrap/update/lint/slim pipelines. `SKILL.md` has principles, always-on floor, and edit steps. `formats.md` holds harness adapters and caps; `patterns.md` lists smells. Invokes on create or edit. `metadata.version` → `0.3.0`.
- `make-docs`: confirm brief headings are English (`Understood`, `Is this correct?`, `Unknowns`); bullets and questions follow the user's chat language.
- `make-docs` and root `README.md`: opening sentences name the job, without mid-sentence bold.
- `make-docs`: spec keywords follow BCP 14 ([RFC 2119](https://www.rfc-editor.org/rfc/rfc2119.html) as updated by [RFC 8174](https://www.rfc-editor.org/rfc/rfc8174.html)). They are ALL CAPS only. Each spec file includes the incorporation sentence.
- `make-docs`: `SKILL.md` is a router (commands, invariants, Done→phase READ). Unattended assume-and-record removed. `update` asks when the stamp is missing or a refactor vs behavior is unclear. Templates mark example rows as replace-or-cut.
- `code-review-plus`: report and persist emit a heading only when the section has content (P0–P3, Dead Code, Test quality, What Looks Good, Author claimed, Manual/UI); `## Fix` is created on first apply, not as an empty placeholder.
- `code-review-plus`: serial fallback (no subagent) restates a running CandidateFinding carry list after each pipeline so auto-compact does not drop earlier hunts.
- `code-review-plus`: fix loads findings from this conversation or `docs/code-review/` memory, reads `## Fix` to skip or re-open stale Closed IDs, and merges the section after apply.
- `code-review-plus`: thinner `SKILL.md` (human-facing one-line description, Commands aliases, Rules cut to secrets); knowns dismiss lives in `references/phases/knowns.md`; test-quality, fix, and prune.
- `code-review-plus`: shape selection on `normal` and `large/sensitive` uses priority (`llm` > `web` > `api` > language for Security/Quality; majority language for Correctness/Architecture/Performance) instead of omitting shapes on multi-tag `normal`.
- `code-review-plus`: report carries `Must NOT change`; Phase 4 fills the skeleton and Phase 4.5 persists before emit; Done criteria live in the phase files (SKILL.md table is the index); Pass B `verification_note` cites files re-read; hunters fall back to serial when the harness has no subagent; report sample moved to `references/examples/report-sample.md`.
- `markdown-writer`: write bar is _scan_ (headings + first sentence) and _parse_ (lists, tables, fences, links as structure); house style and YAML frontmatter stay; `metadata.version` → `0.2.0`.
- `markdown-writer`: rewriting pass on `SKILL.md`, `README.md`, and `references/frontmatter.md` (cut slogan, duplicated Prove restatement, em dashes, and pointer identity the body already carries).
- `markdown-writer`: write-process skill (house style in `SKILL.md`, YAML in `references/frontmatter.md`); renamed from `markdown-editor`; `metadata.version` → `0.1.0`. Root `README.md` lists the skill.
- `markdown-writer`: one-line by default; _prose wrap_ only when dest requires it (MD013, EditorConfig `max_line_length`, or the file already wraps).
- `makefile-expert`: process skill (branches `write` / `review`, kinds `glue` / `compile`) with completion criteria; depth in `references/` (`glue.md`, `graph.md`, `variables.md`); `metadata.version` → `0.1.0`. Root `README.md` lists the skill.
- `makefile-expert`: rewriting pass on `SKILL.md` and `references/` (cut puffery, em dashes, and binary contrast where the rule already stood).
- `.markdownlint.yaml`: `MD010.code_blocks` off so GNU Make recipe examples may use real tabs.

### Removed

- Skill name `write-great-agentsmd`. `npx skills add diegoos/skills --skill write-great-agentsmd` no longer resolves; use `--skill write-great-instructions`.
- `write-great-instructions`: `references/phases/` (`bootstrap.md`, `update.md`, `lint.md`, `slim.md`), `references/lint-checks.md`, and `references/harnesses.md` (merged into `formats.md`).

## [0.1.1] - 2026-08-12

### Changed

- `.markdownlint.yaml`: `MD024.siblings_only` so Keep a Changelog section headings (`Added` / `Changed` / `Fixed`) may repeat under each version.

### Fixed

- `code-review-plus`: Phase 4 report is a skeleton fill of `report.md` — English heading strings, mandatory Findings Overview Markdown pipe table (six columns), prose may be localized; completion criteria and Rules tightened so freeform Resultado/Achados lists no longer satisfy Done.
- `deep-security-review`: Phase 4 report is a skeleton fill of `report.md` — English heading strings, mandatory Findings Overview Markdown pipe table (seven columns), prose may be localized; completion criteria and Rules tightened the same way.

## [0.1.0] - 2026-08-10

### Added

- `deep-security-review`: false-positive pipeline — hunter Pass A bar, verify Pass A intake + expanded checklist/P0 bar/FP table, orchestrator-only `examples/kept-vs-dropped.md`, required `drop_reason` on drop/downgrade.
- `deep-security-review`: fix branch (`fix` / `apply` / `implement`) via `references/phases/fix.md` — apply kept findings with a fix acceptance gate; never re-dispatch domain hunters; never relax auth/validation.
- `deep-security-review` v0.2.0: `DispatchManifest` hotspots, bypasses, and auth*model; hunt angles and universal moves; verify `disprove` section, confirmation gates, P0/P1 `trace`/`intended_behavior`/`trigger_sketch`, and conditional re-verify; report Hardening notes separate from Findings; AuthZ JWT/reset/fail-open deltas; Injection SSRF rebind/TOCTOU and SSTI; web DOM source→sink and origin checks; LLM `\_boundary-crossing*` and confused-deputy framing; Secrets crypto thin; Infra reachability/SoD/SRI; OWASP map awareness header; language-shape CSPRNG probes.
- `code-review-plus`: optional stack shapes for web, API, TypeScript/JavaScript/Node, Python, Go, Rust, and `llm` (`references/shapes/`).
- `code-review-plus`: adaptive dispatch tiers (`trivial` | `normal` | `large/sensitive`) in Phase 1 scope.
- `code-review-plus`: shapes on tier `normal` when exactly one eligible stack tag applies; multi-tag on `normal` omits shapes.
- `code-review-plus`: optional single P0 verifier subagent after Pass B (ambiguity or ≥2 P0-capable candidates); skip documented when Pass B suffices.
- `code-review-plus`: orchestrator-only `dependency-review.md`, structural `remedies.md`, Pass B examples `examples/kept-vs-dropped.md` (stack FP/TP cases), and optional `examples/eval-notes.md` calibration pattern.
- `CHANGELOG.md` (Keep a Changelog) and an `AGENTS.md` rule to record notable changes here on every edit.

### Changed

- `deep-security-review`: Phase 3 FP SSOT moved to `examples/kept-vs-dropped.md` (confirmation gates + recurring FP table + worked cases); verify file points there and stays severity/status/fields/re-verify.
- `deep-security-review`: BusinessLLM dispatch uses checkable signals (tags, payment/wallet hotspots, LLM tools/RAG/MCP, admin agent tools, package-publish) instead of vague "high-value flows".
- `deep-security-review`: severity is P0–P3 with CRITICAL–LOW derived 1:1 (no mismatch); re-verify **dispatches** when triggers fire and **skips** otherwise (no `may`).
- `deep-security-review`: Rules and hunt Pass A use positive framing; hunter self-consistency (working control stays unflagged); secrets/logging audit gaps → Verification Gaps; report Verification Gaps include audit/alert probe.
- `deep-security-review` and `code-review-plus`: fix branch applies **clean** minimal fixes (reuse first, one concept per name, derivability, non-obvious comments only, no unshipped compat / overfitting) with clean-fix checks in the acceptance gate.
- `deep-security-review` and `code-review-plus`: Findings Overview table uses severity/category emojis (🚨 vulnerability · 🔴 P0 · 🟠 P1 · 🟡 P2 · ⚪️ P3).
- `deep-security-review` and `code-review-plus`: empty-review guardrail — when verification yields zero kept findings, state that nothing was found and Approve; do not fabricate report rows (report templates + Rules; CRP replaces the weaker "short approval" line).
- `deep-security-review`: SSOT prune across domains/shapes (JWT → authz, browser exploitation → web, LLM rules → business-llm, supply-chain policy → infrastructure); severity routing (`kept` vulns only get P0–P3; `needs-runtime` → Verification Gaps); `SKILL.md` completion criteria synced to phase files; `metadata.version` → `0.2.0`.
- Root `README.md`: `deep-security-review` blurb and comparison note updated for hotspots, disprove, hardening notes, and `/deep-security-review fix`.
- `global-rules.md`: _tight_ ladder (build-or-not → reuse → stdlib → platform → dep → one-line → min); edge-case-correct at equal size; `ceiling:`/`upgrade:` marker; surgical fix-once / wrong-place warning; challenge X-vs-Y; a11y and data-loss-safe errors; _red_ proof allows assert/self-check; durable still wins for structure; stack and done checklist unchanged.
- Root `README.md`: operating stack for agent rules (global → repo `AGENTS.md` → skills); layered or fused deploy.
- `code-review-plus`: thinner `SKILL.md` (READ + completion criteria per phase); denser perspectives, verify, synthesize, fix, and report template.
- `code-review-plus`: hunter reference budget (`1` perspective + `0|1` shape); Pass A canonicalized in the dispatch prompt; pipeline/shape Pass A limited to domain-specific reminders.
- `code-review-plus`: English-only tier label `large/sensitive` (replaces Portuguese `grande/sensível`).
- `code-review-plus`: prose cleanup for agent docs (less duplication, clearer regression-gate wording, single pointer to `/deep-security-review`).
- Root `README.md`: clearer `global-rules.md`, link to `CHANGELOG.md`, root layout, tighter skill blurbs, `/code-review-plus fix`, and `llm` / normal-tier shape notes.

### Fixed

- `code-review-plus`: false-positive table covers configured formatter/linter style ownership; harder P0 bar and `needs-runtime` handling in verify/synthesize.
