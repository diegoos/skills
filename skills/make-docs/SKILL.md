---
name: make-docs
description: >
  Use when the user wants architecture docs or behavioral specs, asks to
  explore a codebase for documentation, sync docs after changes, or record
  an ADR. Branches: explore (survey, propose, generate), update (since last
  docs stamp → sync), adr (decision record).
---

# Make docs

Produces a documentation suite in `docs/`: **architecture** (how it's
structured) and **specs** (what it does). Specs name only **observable**
outcomes — an agent can implement or verify against them.

## Commands

- **`explore`** — survey codebase, propose structure, generate full suite
- **`update`** — sync docs with commits since the last docs stamp
- **`adr`** — record one architecture decision

## Layout

```
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

By repo size: **small** — README + architecture.md + decisions/;
**medium/large** — full set; **monorepo** — root docs/ + one per service
(nearest wins). Cut any file or section the survey did not **earn**. Fill
every earned section from code evidence — no template stubs left behind.

## Templates

Before writing a file, load its template from `references/`:

| Template | File |
|---|---|
| `references/template-readme.md` | `docs/README.md` |
| `references/template-architecture.md` | `docs/architecture/architecture.md` |
| `references/template-glossary.md` | `docs/architecture/domains/glossary.md` |
| `references/template-api.md` | `docs/architecture/domains/api.md` |
| `references/template-constraints.md` | `docs/architecture/domains/constraints.md` |
| `references/template-adr.md` | `docs/architecture/decisions/ADR-*.md` |
| `references/template-patterns.md` | `docs/architecture/patterns.md` |
| `references/template-spec.md` | `docs/specs/<domain>.md` |

## Specs

Specs describe **observable** behavior — outcomes a user or external system
can see. Name domains after behavior (`auth`, `orders`), not folder layout.

- One requirement = one **SHALL** (split compound requirements).
- Keywords: MUST / SHALL / SHOULD / MAY (RFC 2119).
- Each requirement has at least one Scenario (Given/When/Then) that
  **exercises** it — a concrete case, not a rewording.
- Cover the case that would hurt most to see broken; name it explicitly.
- Pure refactor with no behavior change → no spec update (record that).

## explore

1. **Survey** — stack, runtime, entry points, data stores, API protocol (if
   any), auth (if any), deployment, patterns, quality targets. Identify
   behavioral domains by feature. Read existing docs first.
   **Done when:** stack, runtime, entry points, and deploy named from code;
   auth named only if present; every behavioral domain listed by feature
   name; existing docs read; out-of-scope items flagged or skipped.
2. **Propose** — list files to create; present and ask for approval.
   Unattended (Agent mode): assume the most reasonable list, proceed, and
   record the assumption.
   **Done when:** user confirmed or declined, or assumption recorded.
3. **Generate** — for each file, load its template and write. Write
   README.md last (indexes every other file; set `> Updated on` to today's
   ISO date). Cut what the survey did not **earn**. Fill every earned
   section from evidence.
   **Done when:** every confirmed file written from its template; unearned
   sections omitted; no placeholder stubs in earned sections; stamp set.
4. **Verify** — claims confirmed against code; every ADR names a *why*;
   every requirement has a scenario; quality targets are numbers; diagrams
   match the code they summarize; README indexes every file; earned
   sections are filled from evidence.
   **Done when:** every check above passes.

## update

1. **Scope** — read `docs/README.md` for `> Updated on <ISO-date>`. Count
   commits since that date (`git rev-list --count HEAD --since=<date>`).
   - Missing stamp → ask the user for the range (or offer a full re-sync).
   - Count ≤ 10 → cover all commits since the stamp.
   - Count > 10 → inform the count and ask: cover all, last N commits, or
     a specific base (SHA / date). Wait for the answer before diffing.
   **Done when:** base revision chosen (all since stamp, last N, or
   user-specified base).
2. **Diff** — `git diff <base>..HEAD` plus unstaged/uncommitted changes →
   classify: structural → architecture, behavioral → specs, decision → ADR.
   **Done when:** every changed path classified.
3. **Update** affected files. Load the template before writing. Pure
   refactor → record "no spec change" explicitly. Set `> Updated on` in
   `docs/README.md` to today's ISO date.
   **Done when:** every classified change reflected or explicitly waived;
   stamp refreshed.
4. **Verify** — every behavioral change has spec update or "no spec
   change"; structural changes in architecture.md; diagrams match code;
   cross-references resolve; stamp present and current.
   **Done when:** every check above passes.

## adr

Load `references/template-adr.md`. Number `ADR-NNNN-<slug>.md`. Supersede
with two-way links. If structural boundaries change, update architecture.md.
**Done when:** names a *why*; gains + costs present; alternatives have
reasons; architecture.md updated if boundaries moved.

## Out of scope

Data model, observability, CI/CD. If detected during survey, ask before
generating; otherwise skip.
