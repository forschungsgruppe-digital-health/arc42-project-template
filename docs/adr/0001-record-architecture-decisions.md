# ADR-0001: Record architecture decisions

- **Status:** Accepted
- **Date:** 2026-07-18

## Context

We want the significant decisions that shape this project's architecture and engineering process to be
visible, durable, and reviewable — for humans and for the AI agents that read this repository. Decisions
made only in chat or in a maintainer's head are lost and re-litigated.

## Decision

We record significant decisions as **Architecture Decision Records (ADRs)** in `docs/adr/`, one file per
decision (`NNNN-title.md`), using the format **Context → Decision → Rationale → Consequences** with a
status and date. ADRs are immutable once Accepted; a decision is changed by a new ADR that supersedes the
old one. Section 9 of the arc42 documentation links and summarizes them.

## Rationale

Lightweight, text-based, versioned-with-the-code, and tool-agnostic. The format is the widely used
Nygard/MADR style; it pairs naturally with arc42 section 9 and is understood by the bundled
`arc42-generator` and `docs-auditor` skills.

## Consequences

- Every non-trivial architecture or process decision gets an ADR before or with the change that
  implements it.
- The `arc42-generator` skill folds ADRs into arc42 section 9; `docs-auditor` checks they are linked and
  consistent.
- Superseded ADRs stay in the repo (marked) as a decision history.
