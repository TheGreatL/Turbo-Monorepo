# Guide 04: Testing & Quality Standards

This guide explains the mandatory **Three-Tier Test Equivalence Rule** and code quality baselines enforced in this repository.

---

## 1. The Three-Tier Test Equivalence Rule

Every feature implementation must include tests across all three tiers:

```text
       ▲
      / \
     /   \     Tier 3: End-to-End (E2E) Tests
    /     \    Full user/system journeys across boundaries
   /───────\
  /         \   Tier 2: Supertest (Integration / API Tests)
 /           \  HTTP routes, controllers, middleware, payload schemas
/─────────────\
/               \ Tier 1: Unit Tests
/                 \ Pure domain logic, algorithms, and models in isolation
───────────────────
```

### Tier 1: Unit Tests
* **Target**: Pure calculations, domain models, validations, and helper utilities.
* **Characteristics**: Runs completely in-memory in milliseconds without external I/O, disk, or network calls.
* **Placement**: Placed adjacent to source files (e.g. `user.model.ts` -> `user.model.test.ts`).

### Tier 2: Supertest (Integration / API Tests)
* **Target**: HTTP route handlers, API schemas, authentication middleware, request headers, and status code correctness.
* **Characteristics**: Tests the mounted application service via Supertest (or HTTP harness equivalent) without deploying to external infrastructure.
* **Placement**: Located in an `api.test.ts` or `integration/` directory within the application.

### Tier 3: End-to-End (E2E) Tests
* **Target**: Critical vertical journeys from entry to final state verification (e.g., user signup -> checkout flow -> order placed).
* **Characteristics**: Validates the end-to-end user path against a running instance of the stack.
* **Placement**: Stored in a root or app-level `e2e/` test suite (e.g. Playwright, Cypress, Maestro).

---

## 2. Test-Driven Development (TDD) Lifecycle

1. **RED**: Write an automated test exercising the expected behavior through the public interface. Run it and confirm it fails **for the expected reason**.
2. **GREEN**: Write only the minimum code necessary to make the test pass. Do not add speculative handling.
3. **REFACTOR**: Eliminate duplication and improve structure while keeping tests green across all tiers.

---

## 3. Fowler Code Smells Baseline

Every code change must pass `/code-review` without introducing unaddressed baseline smells:

* **Mysterious Name**: Names that do not clearly describe what a variable, type, or function does.
* **Duplicated Code**: Identical logic hunks across multiple sites. Extract to a shared module.
* **Feature Envy**: A function querying another object's properties more than its own. Move the function to the data.
* **Data Clumps**: Parameters that always travel together. Group them into a dedicated type.
* **Primitive Obsession**: Passing raw strings/numbers instead of strong domain types (e.g. `string` instead of `OrderId`).
* **Shotgun Surgery**: A single logical change that forces edits across dozens of unrelated files. Consolidate into a cohesive module.
