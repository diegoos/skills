# Last-mile glue

Load when Make is the repo CLI: docker, lint, generate, deploy, or other tools.

## Namespace

Name action targets with `/`: `docker/build`, `test/unit`. Put one namespace per included file when the root grows (`tasks/Makefile.docker` for `docker/*`).

`:` inside a target name breaks prerequisite edges. Make parses `docker:build: docker:deps` as other syntax and skips the dependency. Hyphens are readable but do not group as well in `help` output.

```makefile
.PHONY: docker/build docker/push

docker/build: ## Build the image
	docker build -t example/app:$(TAG) .

docker/push: docker/build ## Push the image
	docker push example/app:$(TAG)
```

## Split files

```makefile
-include tasks/Makefile.*
```

The leading `-` means a missing `tasks/` is not an error. Root `Makefile` keeps `.DEFAULT_GOAL`, shared variables, and standard names; namespace files keep their targets.

## Standard names

Root glue files expose a small, stable set so `make` / `make help` is enough to start:

| Target    | Role                                                          |
| --------- | ------------------------------------------------------------- |
| `help`    | Default goal; lists namespaced targets                        |
| `deps`    | Tool / install checks                                         |
| `build`   | Primary build                                                 |
| `test`    | Test suite                                                    |
| `install` | Install (honor `DESTDIR` / `PREFIX` when files are installed) |
| `clean`   | Remove generated files                                        |

Wire them to namespaced work (`build: docker/build`) rather than duplicating recipes.

## Help

`.DEFAULT_GOAL := help`. Document each public target with a trailing `##` on the target line.

```makefile
.DEFAULT_GOAL := help

.PHONY: help
help: ## List public targets
	@awk 'BEGIN {FS = ":.*##"} /^[a-zA-Z0-9_\/-]+:.*?##/ {printf "  %-24s %s\n", $$1, $$2}' $(MAKEFILE_LIST)
```

## Small targets

A target glues tools. If the body needs loops, `if`, or more than a handful of lines, it is a script:

```makefile
.PHONY: lint
lint: ## Run the linter
	./scripts/lint.sh
```

`deps` can be a real prerequisite of `build` (`build: deps`) so a missing tool fails before the long step.

## Defaults as arguments

```makefile
TAG ?= latest
COMPOSE ?= docker compose

.PHONY: compose/up
compose/up: ## Start the stack
	$(COMPOSE) up -d
```

Call site: `make compose/up TAG=dev`. With no extra flags, the `?=` defaults apply.

## Silence

Prefix with `@` for status lines you want quiet (`@echo`, `@awk` in `help`). Leave build/tool commands visible unless the team already silences them. Skip `.SILENT`.
