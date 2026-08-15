# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- `frontend-design-plus`: ship working web UI (component / app UI / marketing) with origin `greenfield` or `redesign`, Design Read + Lock before markup, routed `reference/` files, anti-slop, and pre-flight tiers A / A+B / A+C.

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
