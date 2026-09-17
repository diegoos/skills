# Shape — Python (PR review)

Hunt language and runtime pitfalls.

## Hunt for

- Mutable default args (`list` / `dict` / `set`) shared across calls
- Bare `except:` or `except Exception: pass` that swallows errors
- Blocking I/O (`requests`, `time.sleep`, sync `open`) inside `async def`, or coroutine called without `await`
- `Any` / unchecked casts that erase a typed boundary the rest of the code relies on
- `eval` / `exec` / `pickle.loads` on untrusted input, or SQL/command strings built by concatenation or unchecked f-strings
- Files, sockets, DB sessions, or locks opened without `with` / `async with` (or equivalent close on all paths)
- If the project configures ruff `C901` or radon, run it on touched functions and cite `file:line` + score

## Pass A

Configured linters own style, import order, and line length. Note `regression_risk` for callers of the changed API.
