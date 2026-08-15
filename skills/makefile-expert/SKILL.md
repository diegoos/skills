---
name: makefile-expert
description: >-
  Author or review GNU Make Makefiles: last-mile glue, incremental/parallel graphs, variable flavors. Use when writing, editing, or reviewing a Makefile, GNUmakefile, make targets, recipes, .PHONY, or a `make` invocation. Branches: write, review.
metadata:
  version: 0.0.1
  author: "Diego Oliveira"
  tags:
    - makefile
    - gnu make
    - make
    - makefile expert
---

# Makefile expert

GNU Make. A Makefile is a _graph_ of files plus last-mile _glue_ across tools. Long programs live in scripts; Make calls them.

Pick a **branch** and state it at the start of the run:

- author or change a Makefile → **write**
- audit an existing Makefile → **review**

Name the **kind** in the same line: **compile** (incremental rebuild of artifacts) or **glue** (task runner / last-mile). Mixed trees are both: glue at the root, compile in the leaf rules. Routed files: [task routing](#task-routing).

## Workflow

1. **Classify.** Branch + kind. Read the existing `Makefile` / `GNUmakefile` and any `include`d files. Record `.DEFAULT_GOAL`, `SHELL`, and whether recipes already use GNU-only features. **Done when:** branch, kind, entry file, and those three facts are named.
2. **Read.** Open the routed files for this kind. **Done when:** those files are in context.
3. **Apply.** Write or review against [Essentials](#essentials) plus the routed refs. Match the repo’s existing layout when it already works. **Done when:** every Essential that applies has a concrete decision in the Makefile or a cited failure.
4. **Prove.** `make -n` on the touched goals (recipes print, nothing runs). Glue: `make help` lists the new namespaced targets. Compile: `make -n -j` shows independent artifacts. **Done when:** those commands exit 0 and the proof matches the change.

## Task routing

| Kind        | When                                            | Read                                    |
| ----------- | ----------------------------------------------- | --------------------------------------- |
| **glue**    | docker, lint, deploy, generate, repo CLI        | [glue.md](references/glue.md)           |
| **compile** | `.o` / binaries, headers, `make -j`, `.d` files | [graph.md](references/graph.md)         |
| **either**  | assignment, `CFLAGS`, override, `$(wildcard)`   | [variables.md](references/variables.md) |

Load `variables.md` whenever the change sets or appends Make variables. Load both glue and graph on mixed trees.

## Branch A — write

1. **Keep the file GNU.** Name it `Makefile`. Use `GNUmakefile` only when GNU-only syntax must not be picked up by another `make`. **Done when:** the filename matches the dialect the recipes need.
2. **Set specials.** Put `.DELETE_ON_ERROR:` and an explicit `.DEFAULT_GOAL` near the top. Glue defaults to `help`; compile defaults to `all` (or the one primary artifact). **Done when:** both lines exist.
3. **Bind variables.** Overridable knobs with `?=`. Immediate values with `:=`. Append flags with `+=` so environment / command-line flags survive. See [variables.md](references/variables.md). **Done when:** every new variable has a _flavor_ and an override story (`make goal VAR=value`).
4. **Name targets.** Glue: _namespace_ with `/` (`docker/build`). Compile: file paths for artifacts, phony names for actions (`all`, `clean`, `install`). **Done when:** every action is in `.PHONY` and glue names are a `/` _namespace_.
5. **Write small rules.** One purpose per target. Prerequisites name the work that must finish first. Loops and branching live in a script the recipe calls. **Done when:** each recipe is a short call to a tool or script.
6. **Close the graph.** Every produced file is `$@`. The recipe updates `$@` on success and returns nonzero on failure. Directories that must exist are order-only (`|`). **Done when:** [graph.md](references/graph.md) (compile) or [glue.md](references/glue.md) (glue) checks that apply are true.

## Branch B — review

Report each failure with target or line. Stay on GNU Make unless the file is already POSIX-only.

- [ ] `.DELETE_ON_ERROR` is set; actions are `.PHONY`
- [ ] `.DEFAULT_GOAL` is explicit (or the first target is the intended default)
- [ ] Recipe lines begin with a tab
- [ ] Each recipe line is a new shell. Shared state uses `&&` / `\` or `.ONESHELL:`
- [ ] `$$` for shell dollars; `$(MAKE)` if a sub-make exists
- [ ] _flavor_ is correct: `:=` unless deferral is required; `?=` for knobs; `+=` for flags
- [ ] Glue targets use a `/` _namespace_ (`docker/build`)
- [ ] File lists use `$(wildcard)` / `$(patsubst)`; complex logic is a script; expansion is ordinary `$(...)`
- [ ] Compile: unique `$@` per config (debug vs release do not share a path); headers via `-MMD -MP` + `-include`
- [ ] `install` prefixes paths with `$(DESTDIR)`; `BINDIR` stays a live prefix (`$(PREFIX)/bin`)
- [ ] `make -n` on the reviewed goals is a legal dry run

**Done when:** every applicable item is checked; each failure cites a target or line.

## Essentials

**Dialect.** GNU Make. Match an existing POSIX-only file only when the repo already requires that dialect.

**Graph over script.** Make is for incremental and parallel rebuilds. A target that always runs a 40-line script is a shell file with extra syntax.

**Recipe tab.** Every recipe line starts with a tab, unless `.RECIPEPREFIX` is set in this file.

**One shell per line.** Make starts a new shell for each recipe line. `cd`, `export`, and shell variables do not survive to the next line unless you chain with `&&` and `\`, or set `.ONESHELL:` on purpose.

**Automatic variables.** Prefer these in recipes: `$@` target, `$<` first prerequisite, `$^` all prerequisites (order-only omitted), `$?` newer prerequisites, `$*` stem. Name an order-only prerequisite explicitly if the recipe needs it.

**Phony actions.** `clean`, `all`, `test`, `help`, `install`, and every namespaced glue target that is not a file: declare `.PHONY`.

**Command-line knobs.** `make docker/build TAG=dev`. Make exports `key=value` arguments. Defaults live in the Makefile via `?=`.

**Fail closed.** Recipes return nonzero on failure. Prefix `-` only on optional cleanup. `.DELETE_ON_ERROR` removes a half-written `$@`.

**Include over recurse.** Share rules with `include` / `-include`. If a sub-make is the only option, call `$(MAKE)` so flags propagate.

**Hard guardrails.** Recipe lines are tabs. Glue target names are a `/` _namespace_. Expansion is ordinary `$(...)`. `CC` / `CFLAGS` / `CXXFLAGS` / `LDFLAGS` are appended or assigned with `?=` so environment and `make VAR=value` still win.
