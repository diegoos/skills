# Hunter: structure

How the system is built. Read layout, entry points, deploy, stores, and load-bearing internals. Skip behavioral requirements (behavior hunter) and prose voice (voice hunter).

## Look at

- Manifests and lockfiles (`package.json`, `go.mod`, `Cargo.toml`, `pyproject.toml`, workspace files)
- Entry points: `cmd/`, `main`, HTTP/server bootstrap, workers, exported library API
- Deploy: Dockerfiles, compose, Helm, IaC, Procfile, `deploy/`
- Stores: database clients, caches, queues, object storage
- Auth wiring only if present (middleware, guards, IAM)
- Module boundaries that a C4 view would need

## Return

```yaml
stack: []                  # languages, frameworks
runtime:                   # named from code or manifest
entry_points:              # path + kind (cli | http | worker | library)
  - path:
    kind:
deploy:                    # path, or unknown
stores: []                 # path + kind; omit if none
auth:                      # absent, or mechanism + enforcement path
views_earned: []           # subset of context, container, component, runtime, deployment
views_cut: []              # views the code does not earn
patterns_in_code:          # only patterns the tree uses
  - name:
    where:                 # path
    cost:                  # one line from the code's tradeoff, or unknown
out_of_scope_detected: []  # data-model | observability | ci-cd when files exist
unknowns: []               # what this lens cannot see
```

Cite a path on every filled field. `unknowns` become confirm questions. A quality number, SLO, or container that is not in the tree stays out of this YAML.
