# Turbo Monorepo

Boilerplate template for monorepo applications.

## Engineering standards & workflows

### Feature implementation

Gold Standard 5-phase lifecycle (Understand -> Seam Design -> TDD -> Two-Axis Review -> Commit/PR). Follow on all feature additions and bug fixes. See `docs/FEATURE_IMPLEMENTATION.md`.

### Coding standards

Deep module design, strict type safety, explicit invariants, and Fowler smell baseline. Enforced during `/code-review`. See `docs/CODING_STANDARDS.md`.

## Agent skills

### Issue tracker

GitHub Issues via `gh` CLI for `TheGreatL/Turbo-Monorepo`. See `docs/agents/issue-tracker.md`.

### Triage labels

Five canonical triage roles (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`). See `docs/agents/triage-labels.md`.

### Domain docs

Multi-context layout (`GLOSSARY-MAP.md` at root pointing to per-package docs). See `docs/agents/domain.md`.
