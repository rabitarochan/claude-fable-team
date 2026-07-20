# Fable Team — HQ Repository Rules

This repository is both the development repository and the headquarters of Fable Team (a Claude Plugin).
The canonical team rules are bundled with the setup skill and imported below:

@skills/setup/rules.md

## Rules Specific to This Repository

- This is **where the framework itself is developed**. Changes to the framework (`agents/` / `skills/` /
  the canonical rules `skills/setup/rules.md`) require user approval and are recorded in
  `CHANGELOG.md` with their evidence signals (the growth-loop discipline)
- Adversarial review of a framework change runs on the **complete change set including the
  CHANGELOG entry draft** — the entry is part of the change; reviewing without it wastes a
  must-fix on its absence
- What ships as the plugin is `.claude-plugin/` + `agents/` + `skills/`.
  State (`.fable-team/`) and documents (README / HANDOFF / CHANGELOG) are not part of the distribution
- After changing the canonical rules, propagate them to already-set-up projects by re-running
  `/fable-team:setup` (replacement between markers)
- Verification procedure: `claude plugin validate .` →
  `/plugin marketplace add <path to this repository>` → `/plugin install fable-team@fable-team` →
  `/fable-team:setup` in a real project
- New skill names must not collide with Claude Code built-in slash command names — a colliding
  base name makes the skill un-invocable even with the fable-team: prefix. Check the current
  built-in list (code.claude.com/docs/en/commands.md) before naming (evidence: 2026-07-20 rename
  of init/resume/debug)
- `README.md` and `README.ja.md` are paired enumeration points — any change to one (structure tree, counts,
  skill/agent listings) must be synced to the other in the same change set
- **This repository is public. Never write real project names or any identifying details of
  private field projects into it** — not in CHANGELOG, growth files, docs, or commit messages.
  Anonymize ("project A / B"); paraphrase or mask evidence quotes the same way. This is the
  Boundary Hygiene outbound rule applied to project identity (hard prohibition by the owner,
  2026-07-08)
