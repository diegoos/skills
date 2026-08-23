# Generic vs earned

Orchestrator-only. Use when confirm or verify is deciding whether a sentence belongs in `docs/`.

## DROP: skill meta in the artifact

Specimen (Portuguese generated README). The tell is skill-meta, not the language.

```text
**Premissa desta suíte:** repositório de tamanho médio. A suíte completa foi gerada, sem contrato de API de rede. Specs descrevem só comportamento observável da CLI e do catálogo remoto. Modelo de dados, observabilidade e CI/CD ficaram de fora, conforme o escopo do `make-docs`.
```

Why: portable to any repo; names this skill; records a size verdict and omitted files inside the documentation. That content belongs in the confirm chat, not in `docs/README.md`.

## KEEP: index what exists

```markdown
# skills documentation

> Updated on 2026-08-22

CLI and skill catalog. Architecture covers the layout under `skills/` and the root policy files. Specs cover install via the skills.sh CLI and the catalog listing.

## Architecture (how it's structured)

- [architecture/architecture.md](architecture/architecture.md)
- [architecture/domains/glossary.md](architecture/domains/glossary.md)
- [architecture/decisions/](architecture/decisions/)

## Specs (what it does)

- [specs/cli.md](specs/cli.md)
- [specs/catalog.md](specs/catalog.md)
```

Why: names this repo; lists only files that exist; no premise; no narration of what was skipped.

## DROP: copied template numbers

A constraints table with `99.9%` availability or `p99 < 200ms` when no config, test, or comment states those numbers.

## KEEP: earned constraint

A row whose target is copied from a file the survey cited (Dockerfile memory limit, test timeout, SLA comment). No source: the section is absent.
