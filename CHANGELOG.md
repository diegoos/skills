# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- `frontend-design-plus`: execution modes (`full`, `solo`, `fast`), capability fallbacks, browser/DOM/static verification levels, a visual quality rubric, custom visual-language registers, and textual quality cases for calibration.
- `frontend-design-plus`: Implement and QA now return shared verification and rubric blocks; performance claims distinguish `guided`, `measured`, and `verified`.
- `frontend-design-plus`: ship working web UI (component, app UI, marketing). Origin from disk (`greenfield`, `redesign`, `polish`). Unanswered fields use `AskQuestion` one per turn unless invent-all. Greenfield marketing Look is unnamed `you-decide` unless the prompt names a catalog `id` or Item number; Direction runs Pick after Frame. App UI skips Look (`style=none`) unless the user named an `id`. Theme is Light / Dark / Both (`system` ships two modes and a chrome switch). Palette asks when hue has no owner; dark `--surface` stays charcoal unless the user named a tinted field. After answers: Design Read + Lock, refs via `load-map.md`, DESIGN.md follow-or-generate, default `index.html` + `main.css` + `main.js`, written *crit*, pre-flight A / A+B / A+C. Slop test splits by task type: marketing keeps logo-swap and occupancy-from-*objects*; app UI keeps dashboard scaffold tells and named recipes (`queue-home`, `list-filter`, `editor`, `accounts`) as a productivity formula rather than a poster. Greenfield marketing commits `folds=` from leftover *objects*. Redesign asks Aim, Keep, and Scope. Polish writes a craft audit against existing refs and closes P0/P1. App UI chrome follows `surfaces.md`. Thirty named style paths for marketing craft when *tension* requires a look.
- `frontend-design-plus`: `reference/composition.md` — marketing greenfield and redesign: *job* → *objects* → P0 → pattern → hierarchy → *kinship* → three occupancy cards (distinct *joins*) → *frame* → *thesis* → `folds=` before style Pick.
- `frontend-design-plus`: briefing field **Scene** on greenfield marketing (occupancy sentence, remembered page, or `You decide from the brief`). App UI, redesign, and polish skip it. Look no longer owns occupancy.
- `frontend-design-plus`: `reference/dispatch.md` — after the Briefing card, parent dispatches Direction / Implement / QA as child agents when the harness has that tool (in-process only when it does not). Packet schema is the hand-off. Isolated component skips dispatch.
- `frontend-design-plus`: `reference/implement.md` — Implement composes from the Packet *thesis*; does not open `anti-slop.md`.
- `frontend-design-plus`: Packet fields `job=`, `P0=`, `pattern=`, `tension=`, `discarded=`, `object-swap=`, `fallback=`, `folds=` on marketing greenfield/redesign. Two-mass first viewport (`break=none`) is valid.
- `frontend-design-plus`: marketing greenfield/redesign Packet **Sketch** (12-col ASCII, footer `join=` / `tracks=`). Same block in DESIGN.md **Layout**. Implement returns `See:` / `tracks=` / `proof=` and marks masses with `data-mass`. App UI returns `main=` / `proof=` (`See:` stays marketing). App UI and polish: `Sketch=none`.
- `frontend-design-plus`: Packet `object-swap=n/a` when Inventory has fewer than two domain nouns; a `because` line on a thin brief fails. Three distinct *joins* still run. App UI Implement `main=` maps `recipe=` (`none` → settings shell).
- `frontend-design-plus`: Packet `first-join=` on marketing greenfield/redesign. The surviving Sketch `join=` must differ. Custom visual-language Craft slots generated from the object. Implement `distinct=` names three category scaffolds and one markup or CSS fact that kills each. Quality case for custom register vs catalog costume.

### Changed

- `frontend-design-plus`: parent scores every briefing field in one pass, then sends remaining blanks in one structured question call when the host tool allows. Serial fallback records `questions=serial`. `execution-modes.md` opens at dispatch, not at Classify. `solo` closes slot files before the next slot.
- `frontend-design-plus`: unnamed marketing Look is catalog-last. Pick uses a catalog `id` only when *tension* matches a When; otherwise `style=custom` or `style=none`. Load map attaches `visual-language.md` before the Catalog on `you-decide`.
- `frontend-design-plus`: leftover marketing folds take the form the object asks for. `layout-patterns.md` first-three-folds stays a lookup when the form is not obvious. Icon+title+blurb grids fail unless the Inventory object is a catalog of items.
- `frontend-design-plus`: marketing Implement always attaches `performance.md`. First viewport must show the primary CTA without scroll and keep the H1 to two desktop lines. A component kit does not define the look. Unused browser/screenshot this run is P1. Rubric Honesty `0` is P0. Distinctness requires a DOM or CSS fact.
- `frontend-design-plus`: orchestration is tool-neutral and mode-aware. Custom visual language is available when a catalog style would become costume.
- `frontend-design-plus`: QA adds evidence-based rubric scoring, distinctness checks, viewport/runtime evidence levels, and explicit unverified limitations. Anti-slop rules now treat punctuation and visual patterns as high-risk tells with justified exceptions instead of universal bans.
- `frontend-design-plus`: Packet requires three distinct *join* tokens from `stack | split | full-bleed | overlap`. `object-swap=` is required when Inventory has ≥2 domain nouns; otherwise `n/a`. Implement maps Frame joins to tracks; the hero-family menu is gone. Crit Q1 and anti-slop test the Packet `object-swap=` line against the DOM unless the line is `n/a`.
- `frontend-design-plus`: Pick refuses the model-default triad (cream+serif+terracotta, near-black+one acid, broadsheet) on `you-decide` unless *tension* names that axis. Enter is the subject's characteristic thing. Deletion check names one leftover craft accessory. QA walks a real render when the harness has one; unverified is not a fail. Label-in-Name (SC 2.5.3) and space-before-cards land in production-engineering / product-register. Generate DESIGN.md retunes one token role when palette+type would pass on any similar page.
- `frontend-design-plus`: marketing occupancy cards must differ in *topology* (join), not column ratio. Packet `folds=` lists leftover *objects*. Crit Q1 / anti-slop / pre-flight use *object-swap* instead of a `7/12` gate. The `asset ≥7/12` formula stays once in composition Frame as labeled fallback.
- `frontend-design-plus`: Direction child is the default when the harness has a child-agent tool. Parent validates Packet only. Direction marketing no longer attaches `layout-patterns.md`. Direction app UI no longer attaches `ux-principles.md`. Dispatch Work is a pointer to slot done criteria.
- `frontend-design-plus`: app UI maps CMS/CRM/home/list/editor/accounts onto the four existing recipes. Packet requires `recipe=` on those views. Scan-10s operator questions, persist verb, filters on the list plane, and queue-in-`main` are the productivity bar.
- `frontend-design-plus`: briefing Scene's two occupancy readings differ in topology (stack vs split vs full-bleed).
- `frontend-design-plus`: Direction treats a named style as a craft path after *tension*. The *thesis* is this product's experience plus occupancy in DESIGN.md Layout. Style Path step 1 confirms Frame occupancy and Packet folds. Anti-slop marketing opens on the *thesis*. `ux-principles.md` drops textbook pillars.
- `frontend-design-plus`: *composition* draws *kinship* rectangles before occupancy cards. Lock `scene=` quotes briefing Scene or the derived sentence. Style Commit does not rewrite occupancy. Anti-slop, crit Q1, and pre-flight B check Packet masses (two-mass page allowed).
- `frontend-design-plus`: `after-briefing.md` orchestrates only (Briefing card, print Lock, dispatch, resume P0). `load-map.md` attaches paths per slot. Parent does not open composition, Catalog, anti-slop, crit, or pre-flight except an isolated component.
- `frontend-design-plus`: `you-decide` / invent-all Scene derives occupancy from *objects* and *kinship*. Pick matches *tension* to a *frame* mass, or `style=none`. QA records findings and does not edit; parent resumes Implement. Object-swap still reading pauses Direction unless the line is `n/a`.
- `frontend-design-plus`: Crit Q1 is geometric — `|measured − Sketch| ≤ 1` column; missing `tracks=` fails (not unverified). Folds stay closed until `tracks=` exists. Parent re-dispatches Implement when the proof block is missing; Direction when `See:` names the wrong object. `object-swap=` tests measured enter against the Sketch unless the line is `n/a`.
- `frontend-design-plus`: briefing still asks Use (Lock `density=`). Unnamed Behave and Constraints are owner `none` (`motion=still`) unless the prompt named motion, states, or artifacts. `valid-packet` is a short fail list. Anti-slop opens on what must be on screen; the duplicate AI aesthetic table was removed. `#first-three-folds` is a lookup rather than a menu.

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
