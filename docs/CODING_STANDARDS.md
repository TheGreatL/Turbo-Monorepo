# Coding Standards: The Gold Standard

This document defines the foundational engineering standards for this repository. These standards are enforced during `/code-review` along the **Standards** axis, complementing automated compiler and linter checks.

---

## 1. Deep Module Design

Every unit of code (function, module, package, service) must maximize **depth**:

* **Small Interface, Deep Implementation**: Expose the smallest possible surface area to callers while encapsulating significant capability and complexity. Avoid shallow pass-throughs.
* **Stable Seams**: Place interfaces at natural seams where behavior can be adapted or substituted (e.g. in tests) without editing callers.
* **Locality of Knowledge**: Changes, edge cases, and business invariants must be isolated within the module that owns them. Callers should never have to orchestrate another module's internal state.

---

## 2. Type Safety & Domain Modeling

* **No Primitive Obsession**: Wrap domain concepts in distinct, branded types or objects rather than passing naked primitives (e.g., `UserId`, `OrderId` instead of bare `string` or `number`).
* **Make Illegal States Unrepresentable**: Design data structures and algebraic types so invalid combinations cannot compile.
* **Strict Null & Boundary Checks**: Do not use unsafe type assertions (`as any`, `as unknown as T`) in production code. Validate external payloads at the system boundaries before passing data into domain modules.

---

## 3. Error Handling & Invariants

* **Fail Fast & Explicitly**: Guard preconditions at the top of functions. Never swallow errors or return empty defaults to suppress exceptions unless explicitly required by the domain specification.
* **Actionable Errors**: Errors must describe what happened, what was expected, and context (such as IDs or input parameters) needed to diagnose the failure.

---

## 4. Code Smells Baseline

Every change is reviewed against Fowler's code smells (*Refactoring*, Ch. 3):

| Smell | Description | Target Resolution |
| :--- | :--- | :--- |
| **Mysterious Name** | Names that fail to reveal purpose or hold honest meaning. | Rename immediately; murky names indicate murky responsibilities. |
| **Duplicated Code** | Similar logic shapes repeated across hunks or files. | Extract the shared shape behind a unified interface. |
| **Feature Envy** | A function reaching into another object's internal data more than its own. | Move the method onto the module owning the data. |
| **Data Clumps** | The same cluster of parameters travelling together repeatedly. | Bundle into a dedicated parameter or domain type. |
| **Primitive Obsession** | Raw strings/numbers representing distinct domain entities. | Introduce a small domain type or value object. |
| **Shotgun Surgery** | A single logical change requiring edits across many disparate files. | Consolidate related behavior into a cohesive module. |
| **Speculative Generality** | Hooks, parameters, or abstractions added without a present requirement. | Delete unused abstraction; inline until a concrete need arises. |
| **Message Chains** | Deep caller navigation (`a.b().c().d()`). | Hide intermediate calls behind a single method on the primary object. |

---

## 5. Testability & Seams

* **Test Through Public Interfaces**: Tests should exercise modules through their public interface at defined seams, not through internal private methods.
* **Fast & Deterministic**: Unit tests must run locally in milliseconds without unmanaged external network or disk side effects.
* **Isolated Side Effects**: Isolate I/O and external service calls behind adapters so the core domain logic remains purely testable.
