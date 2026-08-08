# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- `code-review-plus`: optional stack shapes for web, API, TypeScript/JavaScript/Node, Python, Go, and Rust (`references/shapes/`), selected on the `large/sensitive` tier (at most one shape per hunter).
- `code-review-plus`: adaptive dispatch tiers (`trivial` | `normal` | `large/sensitive`) in Phase 1 scope.
- `code-review-plus`: orchestrator-only `dependency-review.md`, structural `remedies.md`, and Pass B examples `examples/kept-vs-dropped.md`.
- `CHANGELOG.md` (Keep a Changelog) and an `AGENTS.md` rule to record notable changes here on every edit.

### Changed

- `code-review-plus`: thinner `SKILL.md` (READ + completion criteria per phase); denser perspectives, verify, synthesize, fix, and report template.
- `code-review-plus`: hunter reference budget (`1` perspective + `0|1` shape); Pass A canonicalized in the dispatch prompt; pipeline/shape Pass A limited to domain-specific reminders.
- `code-review-plus`: English-only tier label `large/sensitive` (replaces Portuguese `grande/sensível`).
- `code-review-plus`: prose cleanup for agent docs (less duplication, clearer regression-gate wording, single pointer to `/deep-security-review`).
- Root `README.md`: skills table and structure tree updated for adaptive review, shapes, remedies, and dependency review.

### Fixed

- `code-review-plus`: false-positive table covers configured formatter/linter style ownership; harder P0 bar and `needs-runtime` handling in verify/synthesize.
