# Hunter: voice

How existing prose is written. Read README, `docs/`, `AGENTS.md`, recent commit messages, and comments at entry points. Skip architecture topology (structure hunter) and behavioral SHALLs (behavior hunter).

## Look at

- Dominant human language of prose (not identifiers)
- Heading case, tone (dry, tutorial, conversational)
- Terms already used as domain language
- Mixed-language files (README in one language, `docs/` in another)

Identifiers, paths, and BCP 14 keywords are not language evidence.

## Return

```yaml
language_candidate:        # BCP 47 when clear (en, pt-BR, pt-PT, fr, es, de, it, ja, zh, …)
sources: []                # files that decided the candidate
mix_detected: no           # yes when prose languages disagree
tone:                      # dry | tutorial | conversational | unknown
heading_style:             # sentence-case | title-case | mixed | unknown
glossary_terms_in_use: []  # terms already in README/docs
unknowns: []               # mix with no majority, or no prose to sample
```

A mix with no majority is an unknown, not a blended candidate. Do not pick a language to be helpful.
