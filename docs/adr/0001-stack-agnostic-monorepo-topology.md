# 0001. Stack-Agnostic Monorepo Topology & Multi-Context Modeling

## Context
This repository serves as a base boilerplate for all applications. We need a consistent structural pattern for organizing applications, shared packages, domain vocabulary, and testing standards without prematurely tying the template to a specific language, frontend, or backend framework.

## Decision
1. **Topology**: We adopt an `apps/` (deployable targets) and `packages/` (shared internal libraries) monorepo topology.
2. **Domain Architecture**: We adopt a multi-context domain documentation layout (`GLOSSARY-MAP.md` at the root pointing to context-scoped `GLOSSARY.md` files) rather than a single monolithic glossary.
3. **Engineering Invariants**: Every feature implementation requires test equivalence across three tiers: Unit Tests, Supertest (Integration/API), and End-to-End (E2E) Tests, enforced through the Gold Standard 5-phase lifecycle and automated `/code-review`.

## Consequences
* Applications and shared libraries maintain clear physical and logical boundaries.
* New projects created from this template remain flexible across any tech stack while inheriting standardized agent workflows and quality gates from day one.
