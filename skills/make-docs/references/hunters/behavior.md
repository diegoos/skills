# Hunter: behavior

What a user or external system can observe. Read CLIs, HTTP/RPC surfaces, UI flows, tests, flags, and error paths. Skip C4 structure (structure hunter) and prose voice (voice hunter).

## Look at

- Public commands, flags, help text, exit codes
- HTTP/RPC/GraphQL routes and response shapes actually served
- User-visible UI states (success, empty, error) when a UI exists
- Tests and fixtures that lock a behavior
- Feature names (auth, orders, sync), not folder names

Name domains after behavior. One candidate requirement = one observable SHALL. Prefer the case that would hurt most to see broken.

## Return

```yaml
domains:
  - name:                  # feature name
    observables: []        # command, route, or UI outcome + path
    candidate_requirements:
      - shall:             # one observable
        hurt_most_if_broken:  # named case, or unknown
        evidence:          # path
api_surface:               # none, or protocol + evidence path
unknowns: []               # ambiguous, dead, or test-only behavior
```

Cite a path on every requirement. Put compound or guessed behavior in `unknowns`. Invent no endpoint or flag that the tree does not expose.
