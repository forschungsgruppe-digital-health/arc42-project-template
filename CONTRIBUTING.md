# Contributing

Thanks for contributing! This project uses **trunk-based development** and **automated releases**. Keep
changes small and reviewable.

## Branching & releases

- **`main` is the trunk** and the only long-lived branch; it must always be releasable.
- Work on a **short-lived branch** — `feat/*`, `fix/*`, `docs/*`, `chore/*` — and open a PR into `main`.
- PRs are **squash-merged**, so the **PR title must be a valid
  [Conventional Commit](https://www.conventionalcommits.org/)** (`type(scope): subject`). It becomes the
  commit on `main` and drives the release. A CI check (`pr-title.yml`) enforces this.
  - `feat:` → minor · `fix:`/`perf:` → patch · `feat!:` or a `BREAKING CHANGE:` footer → major (while
    below 1.0, breaking → minor via `bump-minor-pre-major`). Other types (`docs`, `chore`, `ci`,
    `refactor`, `test`, `build`, `style`) don't bump the version.
- **Releases are automated by [release-please](https://github.com/googleapis/release-please)** with
  **SemVer**. Merging to `main` opens/updates a "Release vX.Y.Z" PR; merging **that** PR tags the release,
  publishes the GitHub release, and updates `CHANGELOG.md`, `version.txt`, and version headers.
- **Never edit by hand:** `CHANGELOG.md`, `version.txt`, `.release-please-manifest.json`.

To change the branching or release model, run the **`branching-strategist`** / **`release-manager`**
skills — they present the options and re-scaffold the setup + ADR.

## Making a change

1. Branch off `main`.
2. Make the change; keep the docs in step (see below).
3. Ensure CI is green (PR-title lint, docs link/anchor check, plus any project checks).
4. Open a PR with a Conventional-Commit title; one logical change per PR.

## Documentation

- Architecture docs live in [`docs/arc42/`](docs/arc42/README.md) (one file per arc42 section,
  novice+expert readable). Use the **`arc42-generator`** skill to change them — it keeps the set
  consistent and runs **`docs-auditor`** as the quality gate.
- Record significant decisions as ADRs in [`docs/adr/`](docs/adr/README.md).
- Before a release, run **`docs-auditor`** — it checks the docs are complete, consistent, error-free,
  understandable (novice+expert), and usable, and returns fixes you can apply. Its report is saved to
  `docs/reports/` (see the [reports convention](docs/reports/README.md)).

## Security

- Never commit secrets — keep them in CI/repo settings. Never put real/sensitive data in the repo or a
  prompt.
