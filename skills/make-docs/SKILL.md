---
name: make-docs
description: >-
  Use when the user wants architecture docs or behavioral specs, asks to explore a codebase for documentation, sync docs after changes, refresh existing docs against current code, or record an ADR. Branches: explore (survey, confirm, generate), update (since last docs stamp → sync), refresh (full re-survey vs existing docs/), adr (decision record).
metadata:
  version: 0.2.0
  author: "Diego Oliveira"
  tags:
    - docs
    - architecture
    - specs
    - adr
---

# Make docs

Produces a documentation suite in `docs/`: **architecture** (how it is structured) and **specs** (what it does). Specs name only **observable** outcomes. An agent can implement or verify against them.

**Branches:** explore (survey → confirm → generate → verify). Update (delta since the docs stamp). Refresh (full re-survey vs existing `docs/`). Adr (one decision).

**Invariants:** Every claim in the suite cites a path, an observable command, or a config. Missing evidence: omit the section or ask. One language per suite; code identifiers and BCP 14 keywords (ALL CAPS) stay as in source. Hunters collect; the orchestrator writes. Unearned sections are omitted with no justification paragraph in the artifact.

**Reference budget:** The orchestrator opens a phase file when that phase starts. Each hunter gets exactly **1** hunter file. Orchestrator-only refs (`anti-slop`, `language`, `examples`, templates, confirm / generate / verify) are not hunter paths.

## Commands

| Invocation | Branch | Behavior |
| ---------- | ------ | -------- |
| `/make-docs explore` | **explore** | Survey → confirm → generate → verify |
| `/make-docs update` | **update** | `./references/phases/update.md` then verify |
| `/make-docs refresh` | **refresh** | `./references/phases/refresh.md` (survey → confirm → generate → verify) |
| `/make-docs adr` | **adr** | `./references/phases/adr.md` then verify if architecture.md moved |

Without a subcommand, treat as **explore** when `docs/` is missing or the user asked to generate a suite; treat as **update** when they asked to sync after changes and `docs/` exists; treat as **refresh** when they asked to regenerate existing docs against current code.

## Definition of Done

Done for each phase is the completion criterion in its READ file. Open the next phase file when that criterion is met.

### Branch explore

| Phase | Done when | READ |
| ----- | --------- | ---- |
| Survey | Evidence pack ready (hunters returned or `hunters: none` recorded); existing docs read | `./references/phases/survey.md` |
| Confirm | User confirmed the brief, or answered every unknown | `./references/phases/confirm.md` |
| Generate | Every confirmed file written from its template; unearned sections omitted; stamp set | `./references/phases/generate.md` |
| Verify | Every check in the verify file passes | `./references/phases/verify.md` |

### Branch update

| Phase | Done when | READ |
| ----- | --------- | ---- |
| Update | Every classified change reflected or waived in chat; stamp refreshed | `./references/phases/update.md` |
| Verify | Every check in the verify file passes | `./references/phases/verify.md` |

### Branch refresh

| Phase | Done when | READ |
| ----- | --------- | ---- |
| Refresh | Existing `docs/` reconciled to current code; ADRs kept unless contradicted; stamp refreshed | `./references/phases/refresh.md` |

Refresh runs survey → confirm → generate → verify against the current tree. Its READ file names that sequence.

### Branch adr

| Phase | Done when | READ |
| ----- | --------- | ---- |
| Adr | Names a _why_; gains + costs present; alternatives have reasons; architecture.md updated if boundaries moved | `./references/phases/adr.md` |

## Layout

```text
docs/
  README.md              # includes `> Updated on <ISO-date>`
  architecture/
    architecture.md
    domains/
      glossary.md
      api.md            # only if the project exposes an API
      constraints.md
    decisions/          # ADR-NNNN-<slug>.md
    patterns.md
  specs/
    <domain>.md         # one per behavioral domain
```

By repo size: **small:** README + architecture.md + decisions/; **medium/large:** full set; **monorepo:** root docs/ + one per service (nearest wins). Cut any file or section the survey did not **earn**. Fill every earned section from evidence. Example rows in templates are not defaults.

## Templates

Before writing a file, load its template from `references/`:

| Template | File |
| -------- | ---- |
| `references/template-readme.md` | `docs/README.md` |
| `references/template-architecture.md` | `docs/architecture/architecture.md` |
| `references/template-glossary.md` | `docs/architecture/domains/glossary.md` |
| `references/template-api.md` | `docs/architecture/domains/api.md` |
| `references/template-constraints.md` | `docs/architecture/domains/constraints.md` |
| `references/template-adr.md` | `docs/architecture/decisions/ADR-*.md` |
| `references/template-patterns.md` | `docs/architecture/patterns.md` |
| `references/template-spec.md` | `docs/specs/<domain>.md` |

## Specs

Specs describe **observable** behavior: outcomes a user or external system can see. Name domains after behavior (`auth`, `orders`), not folder layout.

- One requirement = one **SHALL** (split compound requirements).
- Requirement keywords follow BCP 14 ([RFC 2119](https://www.rfc-editor.org/rfc/rfc2119.html) and [RFC 8174](https://www.rfc-editor.org/rfc/rfc8174.html)): English tokens, ALL CAPS only. Full list and the incorporation sentence live in `./references/language.md`.
- Each requirement has at least one Scenario (Given/When/Then) that **exercises** it: a concrete case, not a rewording.
- Cover the case that would hurt most to see broken; name it explicitly.
- Pure refactor with no behavior change: no spec update. Record that in chat, not as filler in the spec file.

## Out of scope

Data model, observability, CI/CD. Survey lists them as unknowns when present. Confirm asks. Otherwise omit the files and do not narrate the omission in `docs/`.
