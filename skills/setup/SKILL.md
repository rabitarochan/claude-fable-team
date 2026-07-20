---
name: setup
description: >
  Set up Fable Team in a project. Use after installing the plugin, when the user says
  "/fable-team:setup", "set up Fable Team", or "install Fable Team in this project".
  Creates .fable-team/ (the state directory) and embeds the team rules into the project's
  CLAUDE.md. Re-running updates only the rules section to the latest version (idempotent).
---

# /fable-team:setup — Project Setup

The plugin brings Fable Team's brains (agents and skills).
This skill sets up the remaining two pieces in the target project — **a place for state** and **always-loaded rules**.

## Steps

1. **Read the canonical rules**: `${CLAUDE_PLUGIN_ROOT}/skills/setup/rules.md`

2. **Create the state directory** (do not touch anything that already exists):
   - `.fable-team/growth/inbox.md` ← copy from `${CLAUDE_PLUGIN_ROOT}/skills/setup/templates/inbox.md`
   - `.fable-team/growth/changelog.md` ← copy from the same `templates/changelog.md`
   - Do not create `.fable-team/missions/` now — the first mission creates it

3. **Embed the rules into the project's CLAUDE.md** (this modifies an existing file, so briefly confirm with the user first):
   - Insert the contents of rules.md wrapped between the `<!-- fable-team:rules:start -->` and
     `<!-- fable-team:rules:end -->` markers
   - **If the markers already exist, replace only the content between them with the latest version**
     (re-run = rules update. Never touch project-specific rules outside the markers)
   - If CLAUDE.md does not exist, create it

4. **Report completion** (in 3 lines):
   - One-shot tasks (single-session) → `/fable-team:task`
   - Long-running tasks (spanning sessions) → `/fable-team:mission`
   - When unsure, decide by asking: Will you continue this tomorrow?

## Notes

- The area between the markers is managed by setup. Project-specific rules (including rules
  harvested by the growth loop) go **outside the markers**
- If this is a git repository, suggest committing the setup
