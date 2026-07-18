# AGENTS.md — &lt;PROJECT NAME&gt;

Operational context for AI coding agents (OpenAI Codex, Cursor, GitHub Copilot, Gemini CLI, and others
that read the open [AGENTS.md](https://agentskills.io) standard). This file is self-contained and
**canonical**: Claude Code reads `CLAUDE.md`, which imports this file via `@AGENTS.md`. On conflict, this
file wins.

> **Template note:** replace every `<PLACEHOLDER>` below. The **Branching & releases**, **Conventions**,
> and **Agent capabilities** sections are pre-filled for this template's defaults (trunk-based +
> release-please/SemVer) and can be changed by re-running the `branching-strategist` / `release-manager`
> skills.

## Project

- **Project:** &lt;one-line description of what this system does&gt;
- **Owner:** &lt;team / organization&gt;
- **Status:** &lt;e.g. early development&gt;

## Tech stack

- &lt;language / framework / runtime — this template is technology-agnostic; fill in your stack&gt;

## Repository map

- `docs/arc42/` — arc42 v9.0 architecture documentation (split, one file per section)
- `docs/adr/` — Architecture Decision Records (context → decision → rationale → consequences)
- `docs/reports/` — dated, immutable skill-run reports (see `docs/reports/README.md`)
- `skills/` — vendor-neutral agent skills (single source of truth; see catalog below)
- `CONTRIBUTING.md` — how to contribute; branching & releases

## Conventions

- **Language:** documentation AND code/config in **English** (single canonical source).
- **Commits & PR titles:** [Conventional Commits](https://www.conventionalcommits.org/) — types drive
  SemVer via release-please. Because PRs are squash-merged, the **PR title** must be a valid Conventional
  Commit (enforced by `.github/workflows/pr-title.yml`).
- **Diagrams:** Mermaid, no colors/styles.
- **Docs:** the arc42 set under `docs/arc42/` is the canonical architecture narrative; keep it
  novice+expert readable and run `docs-auditor` before a release.
- **ADRs:** record significant decisions in `docs/adr/`; section 9 of arc42 links them.

## Branching & releases (trunk-based)

- `main` is the trunk and only long-lived branch; it must always be releasable (ADR-0002).
- Short-lived branches (`feat/*`, `fix/*`, `docs/*`, `chore/*`) → PR into `main`, **squash-merge** with a
  Conventional-Commit title. No `develop`/`release/*` branches.
- Releases are automated by **release-please** with **SemVer** (`bump-minor-pre-major` until 1.0):
  merging the release PR tags `vX.Y.Z`, creates the GitHub release, and updates `version.txt`,
  `CHANGELOG.md`, and version headers (ADR-0003).
- **Never edit by hand:** `CHANGELOG.md`, `version.txt`, `.release-please-manifest.json`.

## Architecture invariants (do not violate)

- &lt;list the rules that must always hold — the single write path, the security boundary, etc.&gt;

## Hard boundaries (NEVER do these)

- NEVER commit secrets; keep them in CI/repo settings. `.env` is gitignored; commit only `.env.example`.
- NEVER put real or sensitive data in the repo or a prompt; use obviously synthetic data.
- &lt;add project-specific boundaries&gt;

## Agent capabilities (skills) — vendor-neutral catalog

The portable form is **Agent Skills** (`skills/<name>/SKILL.md`, [agentskills.io](https://agentskills.io)).
`skills/` is the single source of truth; see [`skills/SKILLS_SETUP.md`](skills/SKILLS_SETUP.md) for wiring.

- **`arc42-generator`** — generate the arc42 docs from code (no speculation) or consolidate scattered
  docs into the split `docs/arc42/`; novice+expert; runs `docs-auditor` as the quality gate.
- **`docs-auditor`** — audit ALL documentation against five bars (complete, consistent, error-free,
  understandable for novice+expert, usable); returns a report + ready-to-apply fixes; read-only.
- **`release-manager`** — set up CI-based release management; first run presents the options and
  scaffolds them (default: release-please + SemVer + Conventional Commits).
- **`branching-strategist`** — set up a branching strategy; first run presents the options and scaffolds
  them (default: trunk-based + squash + protected `main`).
- **`grilling`** / **`grill-me`** — a relentless interview that stress-tests a plan/decision before you
  commit; decisions stay yours.

**How each tool accesses them:**

- **Claude Code** — via `.claude/skills/` (symlinks → `skills/`).
- **OpenAI Codex / Cursor / Gemini** — via `.codex/skills/` (symlinks → `skills/`) or the tool's own path.
- **GitHub Copilot / anything else** — read this catalog and perform the skill's instructions inline; the
  `SKILL.md` files are plain-Markdown role/workflow descriptions.

## Notes for non-Claude agents

- Treat **`AGENTS.md` as canonical**; `CLAUDE.md` only adds Claude-Code-specific supplements.
- If your tool lacks a native skills primitive, open the relevant `skills/<name>/SKILL.md` and follow it
  inline.
