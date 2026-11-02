# Guide 05: Domain Modeling & ADRs

This guide covers how to capture ubiquitous domain language in `GLOSSARY-MAP.md` and document irreversible technical decisions using Architectural Decision Records (ADRs).

---

## 1. Multi-Context Domain Glossaries

In complex monorepos, words often have different meanings in different contexts (e.g. `Account` in billing means a credit ledger; `Account` in authentication means a login identity).

To prevent semantic drift, this repository uses a **multi-context glossary**:

### Root: `GLOSSARY-MAP.md`
The root file acts as an index of all bounded contexts in the monorepo:

```markdown
# Glossary Map

## Contexts
- [Auth](./apps/auth/GLOSSARY.md): Handles user credentials and tokens
- [Billing](./apps/billing/GLOSSARY.md): Handles subscriptions, invoices, and payments
- [Catalog](./packages/catalog/GLOSSARY.md): Product listings and inventory
```

### Context: `GLOSSARY.md`
Inside each app or package, define context-specific terms:

```markdown
# Billing Context

Handles invoicing, payment gateways, and recurring charges.

## Language

**Invoice**:
A formal request for payment issued after order confirmation.
_Avoid_: Bill, payment request

**Subscription**:
An ongoing recurring entitlement to services.
_Avoid_: Membership, recurring plan
```

---

## 2. Architectural Decision Records (ADRs)

ADRs record decisions that are **hard to reverse**, **surprising to future readers**, or the **result of non-trivial trade-offs**.

### Where They Live
* System-wide decisions live in `docs/adr/0001-slug.md`.
* Context-specific decisions live in `apps/<context>/docs/adr/` or `packages/<context>/docs/adr/`.

### ADR Structure
Keep ADRs concise and direct:

```markdown
# 0002. Use PostgreSQL For Persistence

## Context
We need a robust, ACID-compliant relational datastore with JSON support.

## Decision
We choose PostgreSQL with Drizzle ORM over DynamoDB or MongoDB.

## Consequences
* High transactional safety and relational integrity.
* Schema migrations must be managed via migration scripts before deployment.
```

### When to Write an ADR
Only write an ADR if all three are true:
1. **Hard to reverse**: The cost of undoing it later is high.
2. **Surprising without context**: A future engineer might wonder "why was it done this way?".
3. **Real trade-off**: There were valid alternatives and you consciously chose one.
