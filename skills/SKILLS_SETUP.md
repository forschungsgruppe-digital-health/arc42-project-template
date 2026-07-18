# Skills setup

`skills/` is the **single source of truth** for agent capabilities in this repo, using the vendor-neutral
[Agent Skills](https://agentskills.io) format (`skills/<name>/SKILL.md` with `name`/`description`
frontmatter, plus Claude-specific extension fields that other agents safely ignore).

## Bundled skills

- **`arc42-generator`** — generate/consolidate the arc42 docs (`docs/arc42/`); uses `docs-auditor`.
- **`docs-auditor`** — audit all docs (complete/consistent/error-free/understandable/usable); read-only.
- **`release-manager`** — set up CI-based release management (first run asks the options).
- **`branching-strategist`** — set up a branching strategy (first run asks the options).
- **`dependency-scanner`** — set up CI dependency/CVE/supply-chain scanning (first run asks the options).
- **`security-scanner`** — set up CI security review — secrets, SAST, AI PR review (first run asks); installs `security-reviewer`.
- **`security-reviewer`** — read-only security review (STRIDE + checklist + scanner triage → dated report).
- **`grilling`** / **`grill-me`** — a relentless interview to stress-test a plan or decision.

## Tool wiring

- **Claude Code** discovers them via `.claude/skills/<name>` — symlinks into `skills/`.
- **OpenAI Codex / Cursor / Gemini** discover them via `.codex/skills/<name>` — the same symlinks — or the
  tool's own skills path.
- **Any other agent** (e.g. GitHub Copilot): read the catalog in [AGENTS.md](../AGENTS.md) and perform the
  skill's instructions inline.

Adding a skill: create `skills/<name>/SKILL.md`, then add both symlinks
(`ln -s ../../skills/<name> .claude/skills/<name>` and the `.codex` twin) and a catalog line in
`AGENTS.md`. **Never edit the symlinked copies — edit `skills/` only.**

The portable core (`name`, `description`, Markdown body) works across every Agent-Skills-compatible tool.
The Claude-specific fields (`tools`, `disallowedTools`, `model`) are extensions; other agents ignore them.
Read-only skills also state their read-only rule in prose so agents that ignore `disallowedTools` still
honor it.
