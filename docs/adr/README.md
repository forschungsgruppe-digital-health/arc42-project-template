# Architecture Decision Records (ADRs)

This directory records the significant architecture decisions for this project. Each ADR is immutable
once **Accepted**; to change a decision, add a new ADR that **supersedes** the old one (and update the
old one's status).

## Format

Each ADR follows: **Context → Decision → Rationale → Consequences**, with a status
(`Proposed` / `Accepted` / `Superseded by ADR-NNNN`) and a date. Numbering is sequential (`NNNN`).
Section 9 of the [arc42 docs](../arc42/09_architecture_decisions.md) links and summarizes these.

## Index

| ADR | Title | Status |
|-----|-------|--------|
| [0001](0001-record-architecture-decisions.md) | Record architecture decisions | Accepted |
| [0002](0002-branching-strategy.md) | Branching strategy — trunk-based development | Accepted |
| [0003](0003-release-management.md) | Release management — release-please + SemVer | Accepted |

> The `branching-strategist` and `release-manager` skills create/replace ADRs 0002 and 0003 when you
> change those strategies.
