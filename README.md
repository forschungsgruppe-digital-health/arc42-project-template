# arc42 Project Template

A **technology-agnostic GitHub template** for starting a project that is documented with
[**arc42**](https://arc42.org/) from day one and maintained with a small toolkit of **AI-agent skills**.
It ships:

- a **split arc42 documentation skeleton** (`docs/arc42/`, one file per section, novice+expert readable);
- **agent skills** to generate, audit, and evolve that documentation and the project's engineering
  process — portable across Claude Code, OpenAI Codex, Cursor, and Gemini CLI
  ([Agent Skills standard](https://agentskills.io));
- **trunk-based development** and **release-please + SemVer** release automation, pre-wired.

> This is a **template repository**. On GitHub, click **"Use this template"** to create your project,
> then run the skills below to fill it in.

## What's inside

```text
docs/arc42/        arc42 v9.0 skeleton — 14 files (12 sections + index + about-arc42)
docs/adr/          Architecture Decision Records (MADR-style); ADR-0001..0003 seeded
docs/reports/      dated, immutable skill-run reports (convention in docs/reports/README.md)
skills/            the canonical agent skills (single source of truth)
.claude/skills/    symlinks → skills/ (Claude Code discovery)
.codex/skills/     symlinks → skills/ (Codex/Cursor/Gemini discovery)
.github/workflows/ release-please (SemVer), PR-title lint, docs link/anchor check
AGENTS.md          canonical agent context (also read by Claude via CLAUDE.md)
CONTRIBUTING.md    branching & releases, how to contribute
LICENSE            Apache-2.0 (code, skills, CI)
LICENSE-docs.md    CC BY-SA 4.0 (the arc42 documentation)
```

## Bundled skills

| Skill | What it does |
|-------|--------------|
| [`arc42-generator`](skills/arc42-generator/SKILL.md) | Bootstrap the arc42 docs from your code (no speculation) **or** consolidate scattered docs into `docs/arc42/`; novice+expert; runs `docs-auditor` as the gate |
| [`docs-auditor`](skills/docs-auditor/SKILL.md) | Audit ALL docs against five bars — complete, consistent, error-free, understandable, usable — with ready-to-apply fixes; read-only |
| [`release-manager`](skills/release-manager/SKILL.md) | Set up CI release management; first run asks the options (SemVer/CalVer, release-please/…) and scaffolds them |
| [`branching-strategist`](skills/branching-strategist/SKILL.md) | Set up a branching strategy; first run asks the options (trunk-based/GitHub Flow/…) and scaffolds them |
| [`dependency-scanner`](skills/dependency-scanner/SKILL.md) | Set up CI dependency/CVE/supply-chain scanning; first run detects the stack + asks the options (Dependabot/Renovate, Trivy, Scorecard, SBOM) and scaffolds them |
| [`security-scanner`](skills/security-scanner/SKILL.md) | Set up CI security review (secret scanning, SAST, AI PR review); first run asks the options and scaffolds the workflows + installs `security-reviewer` |
| [`security-reviewer`](skills/security-reviewer/SKILL.md) | Read-only security review: STRIDE + checklist + scanner triage → a dated report + fixes; findings are human-confirmed leads |
| [`template-updater`](skills/template-updater/SKILL.md) | Reconcile this repo with the latest template release — pull shared tooling (skills + CI) while preserving your content; opens a PR + updates `.arc42-template.json` |
| [`grilling`](skills/grilling/SKILL.md) / [`grill-me`](skills/grill-me/SKILL.md) | Interview you relentlessly to stress-test a plan or decision before you commit to it |

How each tool finds them: **Claude Code** via `.claude/skills/`, **Codex/Cursor/Gemini** via
`.codex/skills/` (both symlink into `skills/`), anything else via the catalog in [AGENTS.md](AGENTS.md).
See [skills/SKILLS_SETUP.md](skills/SKILLS_SETUP.md).

## Quick start (after "Use this template")

1. Replace the `<PLACEHOLDER>`s in [AGENTS.md](AGENTS.md), [README.md](README.md), and
   `docs/arc42/01_introduction_and_goals.md` with your project's specifics.
2. Run **`arc42-generator`** — it bootstraps the code-derivable arc42 sections and marks the rest
   ⚠️ HUMAN INPUT.
3. Run **`docs-auditor`** — it reports whether the docs are complete, consistent, error-free,
   understandable, and usable, with fixes you can apply.
4. Branching and releases are already set to **trunk-based + release-please (SemVer)** (see ADR
   [0002](docs/adr/0002-branching-strategy.md) / [0003](docs/adr/0003-release-management.md)). To choose
   differently, run **`branching-strategist`** and **`release-manager`**.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the branching, PR, and release workflow.

## Staying up to date with the template

Repos created from this template are disconnected from it after creation (GitHub templates are
one-time scaffolding). To keep the **shared tooling** (skills + CI setup) current without clobbering
your own content, the template ships a lightweight update loop:

- **`.arc42-template.json`** — a stamp recording the template release your repo is aligned with.
- **`.github/workflows/template-sync-check.yml`** — a monthly **drift notifier**: it compares your
  stamp to the template's latest release and opens a tracking **issue** when you're behind (it never
  edits files).
- **`template-updater`** skill — the reconciler: it pulls the shared skills + CI-setup changes into
  your repo **while preserving your content and any customized skills**, opens a PR, and updates the
  stamp. Run it when the notifier issue appears (or any time).

For a *fresh* scaffold that wants mechanical file sync instead, `.templatesyncignore` is a ready
starting point for [`actions-template-sync`](https://github.com/AndreasAugustin/actions-template-sync)
(sync tooling, ignore content). The mature FGDH child repos use the skill + notifier, not mechanical
sync.

## License

Dual-licensed: **Apache-2.0** for code, skills, and CI ([LICENSE](LICENSE)); **CC BY-SA 4.0** for the
arc42 documentation under `docs/arc42/` ([LICENSE-docs.md](LICENSE-docs.md)), honoring arc42's own
license. See each file's context for which applies.
