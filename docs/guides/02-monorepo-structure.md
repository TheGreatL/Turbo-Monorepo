# Guide 02: Monorepo Structure

This guide explains how code, workspaces, and dependencies are organized in this monorepo to maintain high modularity and clean boundaries.

---

## 1. Directory Topology

```text
Turbo-Monorepo/
├── apps/                    # Deployable targets, entrypoints, and applications
│   ├── api/                 # e.g., Backend REST/GraphQL/gRPC service
│   ├── web/                 # e.g., Web frontend application
│   └── mobile/              # e.g., Mobile client application
├── packages/                # Shared internal libraries and tooling
│   ├── domain/              # Core business models, entities, and rules
│   ├── database/            # Schema, migrations, ORM/query adapters
│   ├── api-client/          # Shared type-safe API SDK
│   └── tsconfig/            # Shared compiler/tooling configurations
├── docs/                    # Architecture decisions, standards, and guides
│   ├── adr/                 # Architectural Decision Records (ADRs)
│   ├── agents/              # Agent tracking and tooling configurations
│   └── guides/              # Project usage guides
└── GLOSSARY-MAP.md          # Multi-context domain mapping
```

---

## 2. Apps vs. Packages

### What Belongs in `apps/`?
An **App** is an executable or deployable unit. It represents a system boundary or an end-user deliverable:
* Web applications (Next.js, Vite, Astro, Remix, Vue)
* Backend servers & microservices (Node, Go, Python, Rust)
* Mobile applications (React Native, Flutter, Swift, Kotlin)
* CLI tools, scrapers, and background queue workers

**Rule**: Apps should be thin orchestrators. They wire up infrastructure, handle transport (HTTP/gRPC/CLI arguments), and invoke core domain modules from `packages/`.

### What Belongs in `packages/`?
A **Package** is a reusable internal library with a clear responsibility:
* **Domain**: Pure business rules and models with zero framework dependencies.
* **Database**: Schema definitions, migration scripts, and database repository adapters.
* **UI / Design System**: Reusable buttons, layout wrappers, and design tokens.
* **Tooling / Config**: Shared linting configs, base tsconfigs, or build scripts.

---

## 3. Deep Modules & Boundary Rules

To prevent monorepos from degenerating into tightly coupled spaghetti:

1. **Expose Narrow Public Interfaces**:
   Every package should export only what callers need from an explicit entrypoint (e.g. `index.ts`). Internal implementation helpers must not be reachable via deep relative imports (e.g., `import ... from 'packages/database/src/internal/helpers'`).
2. **One-Way Dependency Flow**:
   * `apps/` may import from `packages/`.
   * `packages/` **must never** import from `apps/`.
   * Shared packages should form an acyclic dependency graph (`A -> B -> C`, never circular).
3. **Seams for Testing**:
   Design packages so that any external dependency (network, filesystem, third-party API) is injected through an interface seam, making both unit and integration tests fast and deterministic.
