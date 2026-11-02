# Feature Implementation Guide: The Gold Standard

This document defines the required engineering lifecycle for implementing features and bug fixes in this repository. Every agent and developer must follow this process from task start to completion.

---

## The 5-Phase Implementation Lifecycle

```text
1. Understand & Anchor ──► 2. Seam & Interface Design ──► 3. TDD (Red-Green-Refactor)
                                                                     │
                                 5. Commit & PR ◄── 4. Two-Axis Review ◄┘
```

---

### Phase 1: Understand & Anchor
Before touching or writing any production code:

1. **Locate the Ticket / Spec**:
   * If working from an issue, fetch its requirements via the tracker (`gh issue view <n>`).
   * Explicitly restate the ticket goal and its acceptance criteria.
2. **Consult Domain Documentation**:
   * Read `GLOSSARY-MAP.md` and the relevant context `GLOSSARY.md`. Use canonical domain terms; do not introduce conflicting synonyms.
   * Check `docs/adr/` for existing Architectural Decision Records that constrain or guide this area.
3. **Verify the Fixed Point**:
   * Ensure your branch is rooted at a clean state with passing tests.

---

### Phase 2: Seam & Interface Design
Design before coding. Keep modules deep:

1. **Design the Interface First**:
   * Draft the public function signatures, types, or module boundaries before writing internal logic.
   * Strive for **Depth**: small, simple surface area hiding substantial internal complexity.
2. **Establish the Seam**:
   * Identify the exact seam where this code plugs in. Ensure dependencies can be passed or substituted easily for fast, deterministic unit testing.

---

### Phase 3: Test-Driven Development (TDD) & The Three-Tier Test Rule
Every feature implementation requires test equivalence. No feature is complete without corresponding tests across the three testing tiers:

1. **The Three Testing Tiers**:
   * **Unit Test**: Test business logic, pure calculations, algorithms, and domain models in complete isolation. Fast, deterministic, in-memory execution at module seams.
   * **Supertest (Integration / API Test)**: Test HTTP endpoints, API contracts, middleware, route controllers, and status codes using Supertest (or framework equivalent) against the mounted application without external mocks.
   * **End-to-End (E2E) Test**: Test end-to-end user and system journeys across the entire application stack, verifying real state persistence, auth flow, and full vertical workflows.

2. **The TDD Cycle (Red-Green-Refactor)**:
   * **RED**: Write an automated test exercising the expected behavior through the public interface. Run it and verify that it fails **for the expected reason**.
   * **GREEN**: Write the minimum production code necessary to make the test pass.
   * **REFACTOR**: Clean up the implementation: eliminate duplication, enforce deep module boundaries, and ensure all tests stay green across all 3 tiers.

---

### Phase 4: Continuous Verification & Two-Axis Review
Completion requires both automated validation and architectural review:

1. **Deterministic Verification**:
   * Run typechecking across the project.
   * Run the targeted test suite.
   * Run the complete project test suite to guard against regressions.
2. **Two-Axis Review (`/code-review`)**:
   * Execute `/code-review` comparing your changes against the base branch (`HEAD` vs base):
     * **Axis 1 (Standards)**: Checks compliance with [`docs/CODING_STANDARDS.md`](./CODING_STANDARDS.md) and Fowler code smells.
     * **Axis 2 (Spec)**: Confirms that all ticket requirements are met and no scope creep was introduced.
   * Address all reported violations before claiming completion.

---

### Phase 5: Atomic Commits & PR
Deliver the work cleanly:

1. **Atomic Commits**:
   * Write clear, conventional commit messages (`feat: ...`, `fix: ...`, `refactor: ...`).
2. **Pull Request Quality (`/pr`)**:
   * If opening a PR, invoke `/pr` to generate a structured PR body containing:
     * Summary of change.
     * Before/after proof (terminal logs or test outputs).
     * Reversible vs one-way decision assessment.
