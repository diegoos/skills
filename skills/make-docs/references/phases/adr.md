# Adr

Record one architecture decision. Load `references/template-adr.md`, `references/language.md`, and `references/anti-slop.md`.

## Steps

1. If the *why* is unclear, ask and wait. Leave the constraint unwritten until the user names it.
2. Number `docs/architecture/decisions/ADR-NNNN-<slug>.md` (next free NNNN). Same language lock as the suite.
3. Fill Context, Decision, Consequences (gains + costs), Alternatives considered (each with a rejection reason).
4. Supersede with two-way links when this ADR replaces another.
5. If structural boundaries change, update `docs/architecture/architecture.md`.
6. Anti-slop on Context and Decision: portable sentences and skill meta stay out of the file.
7. READ `references/phases/verify.md`.

## Completion criterion

The file names a *why*. Gains and costs are present. Alternatives have reasons. architecture.md is updated if boundaries moved. Language lock holds. Every check in the verify file passes.
