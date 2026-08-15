# Variables and flavors

Load with any Makefile that assigns, appends, or overrides variables.

## Flavors

| Operator | When it expands                                                    | Use                                                                           |
| -------- | ------------------------------------------------------------------ | ----------------------------------------------------------------------------- |
| `:=`     | Immediate, at the assignment                                       | Default. Literals, paths, results of `$(wildcard)` / `$(shell)` you want once |
| `=`      | Deferred, at each use                                              | Only when the right-hand side must see variables defined later                |
| `?=`     | Assigns only if the variable is still unset; the value is deferred | Overridable knobs: `CC`, `PREFIX`, `TAG`, `PKG_CONFIG`                        |
| `+=`     | Appends; keeps the existing flavor                                 | Extra flags on top of environment / command-line values                       |
| `!=`     | Immediate shell assignment                                         | Rare; prefer `:= $(shell ...)` when you already have that pattern             |

`?=` on an unset variable creates a deferred (`=`) variable. Fine for `CC ?= gcc`. If you need a simple-expanded default, assign with `?=` then snap with `VAR := $(VAR)` only when expansion cost or `$(shell)` duplication is real.

Undefined variables expand to empty. Trailing spaces on a value are kept; leading spaces on the next line of a split assignment are stripped.

```makefile
CC ?= gcc
PKG_CONFIG ?= pkg-config

# Immediate: pkg-config runs once
OPENSSL_CFLAGS := $(shell $(PKG_CONFIG) --cflags openssl)
OPENSSL_LIBS := $(shell $(PKG_CONFIG) --libs openssl)

CFLAGS ?= -O2 -pipe
CFLAGS += -std=c11 $(OPENSSL_CFLAGS)
```

## Who wins

Precedence, high to low: `override` in the Makefile → command line `make VAR=value` → assignment in the Makefile → environment.

- Use `?=` so a user’s `CC=clang` in the environment survives (cross-compile toolchains rely on this).
- `CC = gcc` clobbers the environment; only the command line still wins.
- `override` beats the command line. Use it only when the Makefile must pin a value.

```makefile
# User: make docker/build TAG=dev
TAG ?= latest
```

## Flags

Keep the implicit-rule names: `CC`, `CXX`, `AR`, `AS`, `CFLAGS`, `CXXFLAGS`, `CPPFLAGS`, `LDFLAGS`, `LDLIBS`.

Append project flags so environment and command-line flags survive:

```makefile
CFLAGS := $(CFLAGS)
CFLAGS += -Wall -Wextra
```

The first line snaps a recursive `CFLAGS` from the environment into a simple variable so `+=` cannot loop. Call tools through variables (`$(AR)`, `$(PKG_CONFIG)`), not bare `ar` / `pkg-config`.

## Reference form

Write `$(VAR)` (or `${VAR}`). `$V` is only for a one-character name. In a recipe, `$$` is a literal `$` for the shell (`echo $$HOME`, `awk '{print $$1}'`).

## Target- and pattern-specific

```makefile
debug: CFLAGS += -g
%.o: CPPFLAGS += -Iinclude
```

The extra value applies to that target (and its prerequisites, for target-specific) only.

## Lists and wildcards

`$(wildcard *.c)` is the file list. A bare `*.c` in a prerequisite list is a fallback glob: if nothing matches, Make keeps the literal `*.c`.

```makefile
srcs := $(wildcard src/*.c)
objs := $(srcs:.c=.o)
```

Prefer `$(wildcard)` / `$(patsubst)` / suffix replacement over `$(shell ls ...)`. `$(shell find ...)` is acceptable when the tree is deep and the result is assigned with `:=`.

## Install layout

Overridable dirs, `DESTDIR` only in the recipe:

```makefile
PREFIX ?= /usr/local
BINDIR ?= $(PREFIX)/bin
DATADIR ?= $(PREFIX)/share
MANDIR ?= $(DATADIR)/man

.PHONY: install
install: program
	install -d $(DESTDIR)$(BINDIR)
	install -m 755 program $(DESTDIR)$(BINDIR)/program
```

`DESTDIR` is a recipe prefix only. Packaging tools pass it at install; `BINDIR` stays a live prefix path (`$(PREFIX)/bin`).
