# Generate

Write the confirmed file list. Load, for each file, its template from the SKILL.md table, plus `./references/language.md` and `./references/anti-slop.md`. Hunters do not run in this phase.

## Order

1. Architecture files the confirm list accepted (`architecture.md`, glossary, api, constraints, patterns, ADRs only when confirm asked for a first ADR).
2. One spec file per confirmed domain.
3. `docs/README.md` last: index every file actually written; set `> Updated on` to today's ISO date.

## Fill from evidence

Every earned section is filled from the evidence pack plus the code those paths name. Replace every template placeholder. Example rows in templates are not defaults: substitute from evidence, or cut the row or the whole section.

Omit any file or section confirm did not accept. Omit in silence. No sentence in `docs/` that names this skill, the size verdict, or files left out.

Specs: one SHALL per requirement; each has a scenario that exercises it; BCP 14 keywords stay English and ALL CAPS; the incorporation sentence from the spec template is present; domain names stay the confirmed feature names.

## Completion criterion

Every confirmed path exists and was written from its template. Unearned sections are absent. Earned sections have no placeholders and no example-row leftovers (`Order`, Hexagonal, `99.9%` unless the repo states that number). README indexes only files on disk. Stamp is today's ISO date. Language lock holds in all new prose.
