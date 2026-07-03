# Fable Team — HQ Repository Rules

This repository is both the development repository and the headquarters of Fable Team (a Claude Plugin).
The canonical team rules are bundled with the init skill and imported below:

@skills/init/rules.md

## Rules Specific to This Repository

- This is **where the framework itself is developed**. Changes to the framework (`agents/` / `skills/` /
  the canonical rules `skills/init/rules.md`) require user approval and are recorded in
  `CHANGELOG.md` with their evidence signals (the growth-loop discipline)
- What ships as the plugin is `.claude-plugin/` + `agents/` + `skills/`.
  State (`.fable-team/`) and documents (README / HANDOFF / CHANGELOG) are not part of the distribution
- After changing the canonical rules, propagate them to already-set-up projects by re-running
  `/fable-team:init` (replacement between markers)
- Verification procedure: `claude plugin validate .` →
  `/plugin marketplace add <path to this repository>` → `/plugin install fable-team@fable-team` →
  `/fable-team:init` in a real project
