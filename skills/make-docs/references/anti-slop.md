# Anti-slop (docs)

Patterns that make generated architecture and specs read as generic AI. Rewrite matches. Keep a listed pattern when the repo's existing docs already use it.

Load this file in generate and verify. Hunters do not load it.

## Portability test

If a sentence could move unchanged to another repository, cut it or replace it with a fact, mechanism, or path from this tree.

## Evidence bar

A number (latency, availability, RPS, memory) lands only when config, a test, or a comment in the repo states it. No source: omit the row. Do not invent `99.9%` or `p99 < 200ms`.

## Skill meta stays in chat

The artifact describes the system. Confirm holds size, assumptions, and skipped files. Drop any sentence that names this skill, narrates the suite being generated, or justifies an omission ("left out of scope", "the full suite was generated", "suite premise"). Worked drop: `./references/examples/generic-vs-earned.md`.

## Tells

| Pattern | Example | Do instead |
| ------- | ------- | ---------- |
| Banned words | prose, delve, foster, leverage, utilize, facilitate, empower, streamline, robust, cutting-edge, paradigm shift, game changer, tapestry, realm, beacon, multifaceted, meticulous, intricate, paramount, transformative, elevate, embark, supercharge, harness, ever-evolving, seamless | The concrete verb and object from this codebase |
| Throat-clearing | "Here's the thing.", "This document describes.", "Let's dive in." | The system's job in one sentence, then evidence |
| Binary contrast | "This is not a monolith. It's a set of services." | Name the units the tree actually has |
| Importance puffery | "plays a vital role", "stands as a testament", "marks a pivotal moment" | The fact: what the module does, where |
| Superficial `-ing` | "highlighting the team's commitment to reliability" | Cause or consequence the code implements |
| Fake-strong verbs | "serves as a centralized hub for" | "is" / "has" / the module name |
| Forced groups of three | "fast, simple, and powerful" as architecture | The properties this repo enforces |
| Heading restated | H2 "Runtime" then "The runtime view shows how the system runs." | Start with the flow |
| Knowledge-gap filler | "While specific details are limited, it appears the service…" | `unknowns` in confirm, or omit the section |
| Formulaic outlook | "Despite these challenges, the platform continues to evolve" | Cut. End on the last concrete constraint |
| Weasel attribution | "industry best practices", "experts recommend" | Cite the file that enforces the rule |
| Synonym cycling | "the system… the platform… the solution" for one product | Repeat the name in README / go.mod |
| Skill meta | "Suite premise: medium-sized repository." | Nothing in the file; size lives in confirm |
| Em dash as rhythm | decorative `—` in text | Period, comma, or colon. Keep `--` in flags and code |

Filler (`at its core`, `in order to`, `when it comes to`, `it is important to note`) comes out when it delays the point. Keep a phrase when existing docs already speak that way.

## Keep

Voice and terms already in the project's README. Glossary words the voice hunter listed. BCP 14 keywords. File names. A blunt sentence that names this repo's mechanism.
