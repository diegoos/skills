# Verify

Shared by explore, update, refresh, and adr. Load `./references/language.md` and `./references/anti-slop.md`. Load `./references/examples/generic-vs-earned.md` when a sentence looks portable or names this skill.

## Checks

- Every structural claim matches code. Mermaid diagrams summarize units that exist; they do not add containers.
- Every SHALL has a Given/When/Then scenario that exercises it (a concrete case, not a rewording). Each spec file includes the BCP 14 incorporation sentence. Requirement keywords in specs are ALL CAPS; lowercase must/shall/should/may are ordinary text.
- Quality and constraint numbers cite a path. A metric with no source: the row or section is absent.
- Anti-slop: no portable sentence; no skill-meta paragraph; tells in `anti-slop.md` rewritten or cut.
- One language lock. Headings and prose match it. Identifiers and BCP 14 keywords stay in source form. No mixed FR/EN/PT headings.
- `docs/README.md` lists only files that exist. `> Updated on` is today's ISO date (adr may leave the stamp if it did not touch the suite index; explore, update, and refresh always refresh it).
- Cross-references resolve.
- Every ADR written this run names a _why_, with gains, costs, and rejected alternatives.
- `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, or other model-specific files reference the full documentation index on `docs/README.md`.
- Every documentation has no empty sections.

## Completion criterion

Every check above passes. Failures are fixed in the files before reporting done.
