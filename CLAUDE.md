# &lt;PROJECT NAME&gt; — Claude Code Context

@AGENTS.md

> Project context, repository map, conventions, branching/release rules, architecture invariants, and the
> vendor-neutral skills catalog are in the `AGENTS.md` imported above (canonical — also applies to Codex,
> Cursor, Gemini, Copilot). This file supplements **only** Claude-Code-specific working instructions.

## Working with Claude Code

- Skills are auto-discovered via `.claude/skills/` (symlinks into `skills/` — edit `skills/` only):
  `arc42-generator`, `docs-auditor`, `release-manager`, `branching-strategist`, `grilling`, `grill-me`.
- **Bootstrapping a new project from this template:** run `arc42-generator` to draft the arc42 docs from
  code, then `docs-auditor` to check them. Branching and releases are already trunk-based + release-please
  (ADR-0002 / ADR-0003); re-run `branching-strategist` / `release-manager` only to change them.
- **Documentation changes** go through `arc42-generator` (which uses `docs-auditor` as its gate); keep the
  arc42 set novice+expert readable and the version/date in `docs/arc42/README.md` as the single source.
- All changes via a short-lived branch → PR into `main` (trunk-based, squash-merge, Conventional-Commit
  title). Do not hand-edit release-please-owned files (`CHANGELOG.md`, `version.txt`,
  `.release-please-manifest.json`).
