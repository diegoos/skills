# Structure

Every skill under `skills/<name>/` ships `SKILL.md` and `agents/openai.yaml` (ChatGPT/Codex picker name, short blurb 25–64 characters, `allow_implicit_invocation`). Skills with `disable-model-invocation: true` set `allow_implicit_invocation: false`. Optional: `references/` or `reference/`, human `README.md`, `PATTERNS.md`.

```text
.
├── AGENTS.md               # Policy for agents working in this repo
├── CHANGELOG.md            # Keep a Changelog
├── global-rules.md         # Global agent defaults (layered or fused with repo AGENTS.md)
├── README.md
├── docs/
│   └── structure.md        # This layout
├── skills/
│   ├── write-great-instructions/ # Writing guide for harness instruction files
│   │   ├── SKILL.md            # Principles, floor, how to write an edit
│   │   ├── README.md
│   │   ├── agents/openai.yaml
│   │   └── references/
│   │       ├── formats.md      # path, frontmatter, attach, adapter per harness
│   │       └── patterns.md     # works vs anti-pattern smells
│   ├── commit-message/         # Conventional Commits
│   │   ├── SKILL.md
│   │   └── agents/openai.yaml
│   ├── code-review-plus/       # Multi-perspective code review
│   │   ├── SKILL.md            # Router: review vs fix|apply|implement
│   │   ├── README.md           # Human: flow, memory, commands
│   │   ├── agents/openai.yaml
│   │   └── references/
│   │       ├── phases/         # scope, dispatch, verify, synthesize, persist, knowns, fix, prune
│   │       ├── perspectives/   # correctness, security, architecture, quality, performance
│   │       ├── shapes/         # web, api, ts/js/node, python, go, rust, llm (optional, ≤1 per hunter)
│   │       ├── examples/       # kept-vs-dropped, report-sample
│   │       ├── test-quality.md # tests already in the diff (Quality)
│   │       ├── dependency-review.md
│   │       ├── remedies.md
│   │       └── templates/      # final report
│   ├── deep-security-review/   # Deep security review
│   │   ├── SKILL.md
│   │   ├── agents/openai.yaml
│   │   └── references/
│   │       ├── phases/         # plan, hunt, verify-and-synthesize, fix
│   │       ├── templates/      # final report
│   │       ├── domains/        # authz, injection, secrets, infra, business-llm
│   │       ├── shapes/         # api, web, languages, cloud, llm, …
│   │       ├── examples/       # gates, FP table, kept-vs-dropped (Phase 3)
│   │       └── optional/       # OWASP map (on request)
│   ├── make-code/              # XP Simple Design: write / refactor / improve
│   │   ├── SKILL.md
│   │   └── agents/openai.yaml
│   ├── make-docs/              # Architecture + observable specs
│   │   ├── SKILL.md            # Router: explore / update / refresh / adr
│   │   ├── README.md
│   │   ├── agents/openai.yaml
│   │   └── references/
│   │       ├── phases/         # survey, confirm, generate, verify, update, refresh, adr
│   │       ├── hunters/        # structure, behavior, voice (≤3)
│   │       ├── examples/       # generic-vs-earned
│   │       ├── language.md     # suite language lock
│   │       ├── anti-slop.md    # docs prose tells
│   │       └── template-*.md   # architecture, ADR, specs, …
│   ├── makefile-expert/        # GNU Make: write / review
│   │   ├── SKILL.md
│   │   ├── agents/openai.yaml
│   │   └── references/         # glue, graph, variables
│   ├── markdown-writer/        # Write Markdown
│   │   ├── SKILL.md
│   │   ├── README.md           # Spec and lint pointers (human)
│   │   ├── agents/openai.yaml
│   │   └── references/         # frontmatter
│   ├── frontend-design-plus/   # Visual frontend: greenfield / redesign / polish
│   │   ├── SKILL.md
│   │   ├── README.md
│   │   ├── agents/openai.yaml
│   │   └── reference/          # critique, DESIGN.md spec, Operate recipes
│   └── sass-with-bem/          # BEM + Sass/SCSS
│       ├── SKILL.md
│       ├── agents/openai.yaml
│       └── references/
│           ├── conventions.md
│           └── examples.md
└── .opencode/                  # Optional OpenCode agents (not part of the skills contract)
    └── agents/
        ├── ask.md              # Read-only
        └── reviewer.md         # Single-pass review
```
