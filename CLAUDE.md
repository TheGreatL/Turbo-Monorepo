# Turbo Monorepo

Boilerplate template for monorepo applications.

## Rules & engineering standards

### Feature implementation

Gold Standard 5-phase lifecycle (Understand -> Seam Design -> TDD -> Two-Axis Review -> Commit/PR). Every feature requires test equivalence across three tiers: Unit Test, Supertest (API/Integration), and End-to-End (E2E) Test. See `docs/FEATURE_IMPLEMENTATION.md`.

### Coding standards

Deep module design, strict type safety, explicit invariants, 3-tier test equivalence, and Fowler smell baseline. Enforced during `/code-review`. See `docs/CODING_STANDARDS.md`.

## Agent skills

### Issue tracker

GitHub Issues via `gh` CLI for `TheGreatL/Turbo-Monorepo`. See `docs/agents/issue-tracker.md`.

### Triage labels

Five canonical triage roles (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`). See `docs/agents/triage-labels.md`.

### Domain docs

Multi-context layout (`GLOSSARY-MAP.md` at root pointing to per-package docs). See `docs/agents/domain.md`.
