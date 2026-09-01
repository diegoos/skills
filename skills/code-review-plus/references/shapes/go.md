# Shape — Go (PR review)

Hunt language and runtime pitfalls.

## Hunt for

- Unchecked errors on I/O, network, or DB (`_ = err` without a justifying comment)
- Errors returned bare or rewrapped with `%v`/`%s` / `.Error()` instead of `%w` (breaks `errors.Is` / `errors.As`)
- Goroutine with no cancel or shutdown path (leak)
- Concurrent map read/write without mutex or sync type
- Resource opened without `defer Close` on all return paths; HTTP response body not closed
- `panic` (or `Must*`) for recoverable failure across a package boundary; ok only at init / `main` setup
- Secrets, tokens, or keys from `math/rand` instead of `crypto/rand`
- Slice or map stored from / returned to a caller without a defensive copy when the receiver keeps it
- If the project already runs `gocyclo` or golangci-lint `gocyclo`, run it on touched files and cite `file:line` + score; a series of `if err != nil { return err }` is not a complexity finding

## Pass A

- Read `go` from `go.mod` before version-gated advice (loop-var capture in goroutines only if `go < 1.22`)
- Note `regression_risk` for exported API callers
