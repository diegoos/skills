# Incremental and parallel graph

Load when the Makefile builds files and `make -j` should be correct.

## Rebuild rule

Make rebuilds a target when it is missing or older than a prerequisite. Timestamps are the change signal. If you need `make clean` between debug and release, those configs share an output path.

## Unique artifact

Each recipe has one `$@`. That path is unique per configuration. The recipe updates `$@` on success. Failure returns nonzero so `.DELETE_ON_ERROR` can drop a partial file.

```makefile
.DELETE_ON_ERROR:

obj/%.o: %.c | obj
	$(CC) $(CPPFLAGS) $(CFLAGS) -MMD -MP -c $< -o $@

obj:
	mkdir -p $@
```

`obj` is order-only (`|`): create it first, but a directory timestamp must not force every object to rebuild. Order-only names are absent from `$^`.

## Prerequisites

List every file the recipe reads. For C/C++, generate them:

```makefile
deps := $(objs:.o=.d)
-include $(deps)
```

`-MMD -MP` writes a `.d` beside each object. `-include` stays quiet on the first build when `.d` files do not exist yet.

## Pattern vs static pattern

A pattern rule (`%.o: %.c`) is a template for any matching pair. A **static pattern** binds a known list, so only those files match:

```makefile
$(objs): %.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@
```

Prefer static pattern when the object list is already in a variable. Prefer a pattern rule when outputs live in another directory (`obj/%.o: %.c`).

Built-in implicit rules are enough for a flat `foo.c` → `foo` tree: set `CC` / `CFLAGS` and list `program: $(objs)`. Write a custom pattern only when the built-in cannot place the output.

## Parallel

`make -j` is safe when:

- each step’s output path is unique
- that path is `$@` and is written every successful run
- the recipe fails closed
- the Makefile lists all inputs (including generated headers)
- independent subgraphs share no bottleneck (a `mkdir` of the whole tree as a normal prerequisite of every object serializes the build; list dirs as order-only instead)

Leave `-j` to the call site (`make -j`) on compile graphs. Mark a glue target `.NOTPARALLEL` only when its recipes cannot share the tree.

## Recursion

One Make process, many `include`s, is the default. `$(MAKE) -C subdir` hides the subgraph from `-j` and from this Makefile’s prerequisites. If a sub-make is the only option, call `$(MAKE)` so `-j`, `-n`, and other flags pass through. `export` the variables the child must see. `.EXPORT_ALL_VARIABLES` only when the child is a black box.

## Intermediate files

`.INTERMEDIATE` lets Make delete chained temps. `.SECONDARY` keeps them. `.PRECIOUS` keeps them even on interrupt; use it on a named pattern only when a failed partial file is cheaper than losing a long intermediate. Default: `.DELETE_ON_ERROR` and no `.PRECIOUS` on the final `$@`.

## Search path

Prefer an explicit `dir/foo.h` (or `-I` + listed headers) over `VPATH` / `vpath`. Search paths make “which file did Make pick?” a runtime surprise.
