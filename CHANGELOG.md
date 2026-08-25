# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- `frontend-design-plus`: [polish.md](skills/frontend-design-plus/reference/polish.md) slim path for `origin=polish` on marketing and app UI — Focus question when mute, craft audit + Implement + Tier A in one window, no Direction slot. Stay-closed SSOT in [load-map.md](skills/frontend-design-plus/reference/load-map.md#polish). Packet header `Intent` / `Layout` / `Tokens` on greenfield and redesign. Form effort boxes (`autocomplete`, no retype step, app UI P0 without a greeting hop).
- `frontend-design-plus`: skill for landings, dashboards, and components. Classify origin (`greenfield`, `redesign`, `polish`). Marketing infers `character=`, asks one A/B occupancy, then Style yes/no (prints `catalog.md` only after yes). Direction returns a Sketch Packet and DESIGN.md. Implement returns `See:` / `tracks=` / `scale=` (marketing) or `main=` / `proof=` (app UI). QA runs anti-slop, crit, rubric, verification, and pre-flight. Isolated component skips dispatch.
- `frontend-design-plus`: [product-context.md](skills/frontend-design-plus/reference/product-context.md) reads `PRODUCT.md` / AGENTS.md UX / DESIGN.md Overview when present (`evidence=absent` if not). Harden pass (data overflow, i18n `lang`/`dir`, error taxonomy) when Focus or Constraints ask. Anti-slop `rule=` ids. Polish Focus ids `distill` and `copy`. Onboard section on app UI. Resilient text (chips, badges, interruptible motion). Pre-flight boxes for emoji-as-icon, `cursor: pointer`, chip reflow.

### Fixed

- `frontend-design-plus`: routing holes after the Impeccable/Pro Max pass — `product-context.md` on invent-all / empty Job / complete; Packet `focus=`; marketing Implement attaches resilient-text (and Harden when the signal matches); pre-flight boxes no longer require files QA cannot open; polish Harden via [load-map.md](skills/frontend-design-plus/reference/load-map.md#polish); craft audit opens owner files only when load-map attached them.
- `frontend-design-plus`: second routing pass — stay-closed files no longer follow links into composition, briefing, anti-slop, or crit; Packet `constraints=` and optional Lock `questions=serial`; `fast` extras inlined in SKILL.md; isolated component skips Direction and crit; dispatch Direction bullets are origin-gated; catalog stay-closed except Item number or sites+why; execution-modes does not rescore briefing after the card; design-styles Path step 4 is Commit subtraction (QA owns slop/crit).

### Changed

- `frontend-design-plus`: twelve public terms in SKILL.md Words; occupancy jargon stays in composition.md. Polish skips briefing, catalog, and composition. Implement layout-first, 3–4 wrapper extract, token-only CSS after Lock. Verification is run evidence, not a user study.
- `frontend-design-plus`: Implement layout kit is the full Packet + DESIGN.md + Implement rows (`layout-patterns.md` on marketing; `product-register.md` recipe heading on app UI). Parent keeps card, Packet, and return blocks; discards worker walks. Resume after QA still sends the full Packet, not a Lock/Sketch slice.

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
- `global-rules.md`: *tight* ladder (build-or-not → reuse → stdlib → platform → dep → one-line → min); edge-case-correct at equal size; `ceiling:`/`upgrade:` marker; surgical fix-once / wrong-place warning; challenge X-vs-Y; a11y and data-loss-safe errors; *red* proof allows assert/self-check; durable still wins for structure; stack and done checklist unchanged.
- Root `README.md`: operating stack for agent rules (global → repo `AGENTS.md` → skills); layered or fused deploy.
- `code-review-plus`: thinner `SKILL.md` (READ + completion criteria per phase); denser perspectives, verify, synthesize, fix, and report template.
- `code-review-plus`: hunter reference budget (`1` perspective + `0|1` shape); Pass A canonicalized in the dispatch prompt; pipeline/shape Pass A limited to domain-specific reminders.
- `code-review-plus`: English-only tier label `large/sensitive` (replaces Portuguese `grande/sensível`).
- `code-review-plus`: prose cleanup for agent docs (less duplication, clearer regression-gate wording, single pointer to `/deep-security-review`).
- Root `README.md`: clearer `global-rules.md`, link to `CHANGELOG.md`, root layout, tighter skill blurbs, `/code-review-plus fix`, and `llm` / normal-tier shape notes.

### Fixed

- `code-review-plus`: false-positive table covers configured formatter/linter style ownership; harder P0 bar and `needs-runtime` handling in verify/synthesize.
