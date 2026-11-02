# Turbo Monorepo Boilerplate

A stack-agnostic, agent-first boilerplate for monorepo applications.

Designed to serve as the structural and operational foundation for any application architecture, pairing a clean monorepo topology with automated AI agent workflows.

---

## Architecture & Directory Structure

This boilerplate organizes codebases into high-cohesion, low-coupling workspaces without locking into any specific framework or language:

```text
Turbo-Monorepo/
├── .agents/                 # Shared agent skill definitions and configurations
├── apps/                    # Deployable applications, services, or frontends
├── packages/                # Shared internal libraries, tooling, or configurations
├── docs/                    # Architectural decisions, agent specs, and guides
│   ├── adr/                 # System-wide Architectural Decision Records (ADRs)
│   └── agents/              # Configuration for agent tools (tracker, triage, domain)
├── GLOSSARY-MAP.md          # Multi-context domain dictionary mapping
├── AGENTS.md                # Steering instructions for autonomous coding agents
├── CLAUDE.md                # Steering instructions for Claude Code
└── skills-lock.json         # Lockfile for agent skills
```

### Key Structural Principles

* **Multi-Context Domain Modeling**: Rather than a monolithic domain model, this repo defaults to a multi-context glossary (`GLOSSARY-MAP.md`) where each application or shared package can maintain its own ubiquitous language and scoped decisions (`docs/adr/`).
* **Deep Modules**: Components and packages expose minimal, intentional interfaces hiding internal complexity.
* **Separation of Apps and Packages**: 
  * `apps/*`: End-user deliverables, binaries, APIs, or web applications.
  * `packages/*`: Shared modules, design systems, SDKs, or common domain logic.

---

## Agent Engineering Workflows

This repository is pre-configured with agent skills designed to support end-to-end development flows:

### 1. Skill Router
* **`/ask-matt`**: Ask which skill or development flow fits your current task.

### 2. Main Flow: Idea to Ship
1. **`/grill-with-docs`**: Sharpen new concepts, features, or architecture through interactive interview; records findings in `GLOSSARY.md` and ADRs.
2. **`/prototype`**: Validate ambiguous requirements or UI behaviors with throwaway code before committing to a full build.
3. **`/to-spec` & `/to-tickets`**: Break architectural designs into self-contained tracer-bullet issues on GitHub with explicit blocking edges.
4. **`/implement` / `/implement-spec`**: Build tickets in clean contexts driven by **`/tdd`** (test-driven development).
5. **`/code-review`**: Conduct a two-axis review (Standards + Specification) across diffs before merging.
6. **`/pr`**: Format structured pull requests with before/after visual proof and reversible decision context.
7. **`/retro`**: Reflect on sessions to convert process friction into deterministic tooling checks.

### 3. On-Ramps & Maintenance
* **`/triage`**: Evaluate and route incoming issues with canonical roles (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`).
* **`/wayfinder`**: Navigate high-uncertainty architectural exploration by creating and resolving decision maps on the issue tracker.
* **`/diagnosing-bugs`**: Methodically isolate tricky bugs and regressions with reproduction test cases.
* **`/improve-codebase-architecture`**: Scan for module deepening opportunities and maintain clean boundaries.

---

## Prerequisites

Before using or cloning this repository, ensure you have:

1. **Git**: Installed with your identity configured:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your.email@example.com"
   ```

2. **AI Coding Harness**: An environment that reads `AGENTS.md` or `CLAUDE.md` and supports skills (e.g., Google Antigravity, Claude Code, Cursor, Codex).

3. **GitHub CLI (`gh`)**: Required for agent-driven issue tracking, ticketing (`/to-tickets`), and wayfinding:
   * **Windows**: `winget install GitHub.cli`
   * **macOS**: `brew install gh`
   * **Linux**: `sudo apt install gh`
   * **Authentication**: Run `gh auth login` once per machine.
   * *(Note: If you do not use GitHub, run `/setup-matt-pocock-skills` to switch to local markdown issues).*

---

## Getting Started With a New Project

When using this template to start a new application:

1. **Clone & Set Remote**:
   ```bash
   git clone <template-url> <my-project-name>
   cd <my-project-name>
   git remote set-url origin <new-github-repo-url>
   ```

2. **Configure Skills & Tracker**:
   If needed, run `/setup-matt-pocock-skills` to configure or update GitHub issue tracking and domain doc settings.

3. **Explore Flows**:
   Type `/ask-matt` in your agent prompt to determine the best workflow for your next feature or refactor.
