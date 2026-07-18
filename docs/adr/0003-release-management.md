# ADR-0003: Release management — release-please + SemVer

- **Status:** Accepted
- **Date:** 2026-07-18

## Context

The project needs CI-based release management that is language-agnostic (this is a technology-agnostic
template), gives a human gate without manual changelog toil, and pairs with trunk-based development
([ADR-0002](0002-branching-strategy.md)). Options considered: release-please, semantic-release,
changesets, GoReleaser, manual tag + CI, and release-drafter; versioning schemes: SemVer, CalVer,
bundled single-version, independent per-package.

## Decision

Use **[release-please](https://github.com/googleapis/release-please) with SemVer**, driven by
**Conventional Commits**:

- `release-type: simple` in `release-please-config.json`; `version.txt` is the managed version file;
  `.release-please-manifest.json` holds the version map.
- **`bump-minor-pre-major: true`** so the project stays safely in `0.x` (breaking → minor) until we
  deliberately cut `1.0.0`.
- On push to `main`, release-please maintains a "Release vX.Y.Z" PR; **merging that PR** tags the release,
  creates the GitHub release, and updates `CHANGELOG.md` + `version.txt`.
- A downstream `publish` job (guarded by release-please's `release_created` output) is wired but empty —
  add the build/publish/container step when the project ships artifacts.

## Rationale

Language-agnostic (works for any stack via `simple`, or a language preset later); the always-open Release
PR is a natural review checkpoint and changelog preview — safer than semantic-release's fire-on-merge for
a small team, lighter than changesets' per-PR authoring. SemVer gives consumers machine-readable
compatibility signals; manifest mode scales one→many packages without switching tools.

## Consequences

- `CHANGELOG.md`, `version.txt`, and `.release-please-manifest.json` are **release-please-owned — never
  hand-edited**.
- Commit/PR-title hygiene matters: the Conventional-Commit type determines the version bump (enforced by
  the PR-title lint from ADR-0002).
- Deviations, if needed: CalVer for date-driven deliverables; release-please (tag) + GoReleaser for
  binary/container CLIs; changesets for npm monorepos; semantic-release for fully automated npm CD.
- Changed by re-running the `release-manager` skill, which supersedes this ADR.
