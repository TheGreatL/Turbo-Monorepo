# Project Guides

Welcome to the comprehensive documentation guides for this Turbo Monorepo boilerplate. These guides explain how to use, extend, and maintain projects built on this foundation.

---

## How to Use It From Here (TL;DR)

* **When starting a new project**:
  1. Clone this boilerplate: `git clone <template-url> <my-project-name>`
  2. Re-point the Git remote: `git remote set-url origin <new-github-repo-url>`
  3. Run `/setup-matt-pocock-skills` inside your AI chat to configure your new GitHub Issues board and triage labels.
* **When building features**:
  * Simply ask your agent to build a feature or type `/ask-matt` to route your task.
  * The agent will automatically follow the **5-phase Gold Standard lifecycle** (`docs/FEATURE_IMPLEMENTATION.md`), write **3-tier tests** (Unit, Supertest, E2E), and perform **two-axis code reviews** (`/code-review`)!

---

## Guide Index

| Guide | Description |
| :--- | :--- |
| **[01. Getting Started](./01-getting-started.md)** | Step-by-step setup to clone this template, re-point the remote, and initialize your own issue tracker and skills. |
| **[02. Monorepo Structure](./02-monorepo-structure.md)** | Organizing code between `apps/` and `packages/`, enforcing deep module boundaries, and avoiding leaky abstractions. |
| **[03. Agent-Driven Development](./03-agent-driven-development.md)** | How to use `/ask-matt`, `/grill-with-docs`, `/wayfinder`, `/to-spec`, `/implement`, and `/code-review` in daily engineering work. |
| **[04. Testing & Quality Standards](./04-testing-and-quality.md)** | Fulfilling the mandatory Three-Tier Test Equivalence Rule (Unit, Supertest, E2E), TDD cycle, and Fowler code smell baseline. |
| **[05. Domain Modeling & ADRs](./05-domain-modeling-and-adrs.md)** | Using `GLOSSARY-MAP.md` for multi-context domain clarity and capturing key decisions in `docs/adr/`. |

---

## Quick Reference Commands

* **`/ask-matt`**: Ask which skill or development flow fits your current situation.
* **`/setup-matt-pocock-skills`**: Reconfigure your issue tracker or triage labels.
* **`/grill-with-docs`**: Refine a feature idea through an interactive interview and generate ADRs.
* **`/code-review`**: Run a two-axis review (Standards + Spec) on any diff before merging.
