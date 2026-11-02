# Guide 03: Agent-Driven Engineering Workflows

This boilerplate integrates the **Matt Pocock Skill System**, enabling AI agents to act as disciplined pair programmers rather than unconstrained generators.

---

## 1. The Skill Lifecycle

When working on a feature, bug fix, or refactor, follow this flow:

```text
/ask-matt (Route your task)
    │
    ├──► Unclear/Large Scope ──► /wayfinder (Map decision tickets on GitHub)
    │
    ├──► Need Concept Clarity ─► /grill-with-docs (Interview & record ADRs)
    │
    ├──► Complex Prototype ────► /prototype (Throwaway code to test assumptions)
    │
    └──► Ready to Implement ───► /to-spec & /to-tickets (Create tracer bullets)
                                      │
                                      ▼
                                 /implement (Driven by /tdd)
                                      │
                                      ▼
                                 /code-review (Two-Axis: Standards + Spec)
                                      │
                                      ▼
                                 /pr (Format PR body with proof)
                                      │
                                      ▼
                                 /retro (Update standards & tooling)
```

---

## 2. Key Commands & Skills Reference

| Slash Command / Skill | When to Use | What It Produces |
| :--- | :--- | :--- |
| **`/ask-matt`** | Anytime you are unsure which flow to use. | Clear recommendation of next steps. |
| **`/grill-with-docs`** | Refining a feature idea or architectural proposal. | Sharpened requirements, `GLOSSARY.md` terms, and ADRs in `docs/adr/`. |
| **`/wayfinder`** | Tackling a large, foggy architectural epic. | A map issue on GitHub with child decision tickets resolved one-by-one. |
| **`/to-spec` & `/to-tickets`** | Ready to break an idea into executable tasks. | GitHub issues declaring explicit blocking dependencies. |
| **`/implement`** | Building a specific ticket. | Code implemented test-first via `/tdd`. |
| **`/implement-spec`** | Building an entire spec graph in parallel. | Dispatches subagents across the dependency frontier onto an integration branch. |
| **`/code-review`** | Verifying diffs against base branch. | Independent Standards and Spec reports side-by-side. |
| **`/pr`** | Preparing a pull request. | Structured PR summary, before/after evidence, reversible risk check. |
| **`/retro`** | After a complex build session or sideways turn. | Tooling checks and coding standard updates. |

---

## 3. Context Hygiene Best Practices

* **Keep Planning in One Context**: Keep `/grill-with-docs`, `/to-spec`, and `/to-tickets` in an unbroken context session so the agent remembers the rationale when creating tickets.
* **Fresh Context for Implementation**: Once tickets are published to GitHub, start a fresh session (or clear context) for `/implement`. Each ticket is self-contained and fetches its own context from GitHub.
* **Subagents for Heavy Verification**: Skills like `/code-review` automatically dispatch parallel subagents so heavy diff analysis does not contaminate your main chat history.
