# About arc42

[Back to the architecture docs index](README.md)

> **In brief (for newcomers):** **arc42** is a proven, open template for documenting software
> architecture. It gives you **12 sections**, each answering one clear question about the system, so
> readers always know where to look. You do not have to fill every section fully — fill what matters and
> mark the rest.

## How to read these docs

- Each section is its own file (`01_…` through `12_…`), in a fixed order.
- Every section opens with a **plain-language lede** (for newcomers), then **precise detail** (for
  experts). Unfamiliar terms are defined in the [glossary](12_glossary.md).
- Start with [1. Introduction and Goals](01_introduction_and_goals.md) (what + why), then
  [3. Context and Scope](03_context_and_scope.md) (the boundary), then
  [5. Building Block View](05_building_block_view.md) (the structure).

## The 12 sections at a glance

1. Introduction and Goals — what the system is, its quality goals, its stakeholders
2. Architecture Constraints — the fixed rules the design must obey
3. Context and Scope — the system boundary and external partners
4. Solution Strategy — the fundamental decisions and why
5. Building Block View — the static decomposition into parts
6. Runtime View — how the parts collaborate at run time
7. Deployment View — where the software runs
8. Cross-cutting Concepts — concerns that span many parts
9. Architecture Decisions — the significant decisions as ADRs
10. Quality Requirements — testable quality scenarios
11. Risks and Technical Debt — known risks and debt
12. Glossary — the shared vocabulary

## Attribution & license

arc42 was created by Dr. Gernot Starke and Dr. Peter Hruschka and is published under **CC BY-SA 4.0**
(https://arc42.org). This documentation skeleton is a derivative and is likewise licensed CC BY-SA 4.0
— see [../LICENSE-docs.md](../../LICENSE-docs.md).
