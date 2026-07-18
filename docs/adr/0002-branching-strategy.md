# ADR-0002: Branching strategy — trunk-based development

- **Status:** Accepted
- **Date:** 2026-07-18

## Context

The project needs a branching model that is simple for a small team, keeps `main` always releasable, and
feeds the automated release tooling (see [ADR-0003](0003-release-management.md)) cleanly. Options
considered: trunk-based development, GitHub Flow, GitLab Flow, Git Flow, release-branch-per-version, and
Ship/Show/Ask.

## Decision

Use **trunk-based development**:

- `main` is the trunk and the only long-lived branch; it must always be releasable.
- Work happens on **short-lived** branches (`feat/*`, `fix/*`, `docs/*`, `chore/*`) merged via PR into
  `main` with **squash-merge** and **linear history**.
- The **PR title must be a Conventional Commit** (it becomes the squash commit on `main`); enforced by
  `.github/workflows/pr-title.yml`.
- `main` is protected: required status checks (docs link/anchor check, PR-title lint, plus any project
  checks), no force-push/deletion, and — recommended — one review. Branch protection is a repository
  setting an admin applies.
- No `develop` or `release/*` branches.

## Rationale

Fewest moving parts for a small/research team; squash + a Conventional-Commit PR title is the ideal feed
for release-please (one PR = one clean commit on `main` = one correct version bump + changelog entry). It
avoids Git Flow's long-lived `develop` branch, which fights single-source automated releasing.

## Consequences

- Unfinished work is hidden behind flags/config rather than long-lived branches.
- "Fix forward" on `main` rather than maintaining parallel lines (add a release branch per major only if
  you must support an old version).
- Upgrade paths remain open: adopt Ship/Show/Ask as trust grows; add GitLab-Flow environment branches
  only when real staging→prod promotion appears.
- Changed by re-running the `branching-strategist` skill, which supersedes this ADR.
