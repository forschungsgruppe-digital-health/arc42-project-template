# Architecture Documentation (arc42)

> Version 0.1.0 · unreleased · Structured per the [arc42](https://arc42.org/) template **v9.0-EN (July 2025)**.
> This is the single version+date source for the whole architecture documentation set.

> **New here?** Start with [about-arc42.md](about-arc42.md) — it explains what arc42 is and how to read
> these docs. Each section opens with a plain-language lede for newcomers, then precise detail for
> experts.

> ⚠️ This is a **template skeleton**. Run the `arc42-generator` skill to bootstrap the derivable
> sections from your code and to keep the set consistent; sections marked ⚠️ HUMAN INPUT need you.

## Sections

| Section | What's inside |
|---------|---------------|
| [1. Introduction and Goals](01_introduction_and_goals.md) | What this system is, the top quality goals that drive its design, and who cares about it. |
| [2. Architecture Constraints](02_architecture_constraints.md) | The fixed rules the architecture must obey — technical, organizational, and conventions. |
| [3. Context and Scope](03_context_and_scope.md) | The system boundary — which external partners and systems it talks to, and how. |
| [4. Solution Strategy](04_solution_strategy.md) | The handful of fundamental decisions that shape everything else, and why. |
| [5. Building Block View](05_building_block_view.md) | How the system decomposes into parts — the static structure, top-down. |
| [6. Runtime View](06_runtime_view.md) | How the parts collaborate at run time, in the important scenarios. |
| [7. Deployment View](07_deployment_view.md) | Where the software runs — infrastructure, containers, networks, ports. |
| [8. Cross-cutting Concepts](08_concepts.md) | Concepts that apply across many building blocks — security, persistence, logging, error handling, i18n, and so on. |
| [9. Architecture Decisions](09_architecture_decisions.md) | The significant architecture decisions, recorded as ADRs. |
| [10. Quality Requirements](10_quality_requirements.md) | Concrete, testable quality scenarios and the quality tree. |
| [11. Risks and Technical Debt](11_technical_risks.md) | Known risks and technical debt, with mitigations. |
| [12. Glossary](12_glossary.md) | The domain and technical terms used across these docs — the shared dictionary. |
| [about-arc42.md](about-arc42.md) | What arc42 is and how to read this documentation |

## Conventions

- **One file per section**, basenames matching the arc42 golden master.
- **Novice + expert:** every section starts with a plain-language lede, then expert detail.
- **Diagrams:** Mermaid, no colors/styles.
- **ADRs:** in [docs/adr/](../adr/README.md); section 9 links them.
- **Quality gate:** the `docs-auditor` skill checks this set is complete, consistent, error-free,
  understandable, and navigable.

## License

The documentation in this directory is licensed **CC BY-SA 4.0** (see [../LICENSE-docs.md](../../LICENSE-docs.md)),
in keeping with the arc42 template's own license. Code, skills, and CI in this repository are Apache-2.0.
