---
name: judge
description: >
  Apply the Fable Team judgment playbook. Use when stuck on a decision with no right answer —
  patch or refactor, ask the user or keep going, add a dependency or build it yourself, whether
  it's safe to delete code, whether to fix the test or the implementation, when an estimate has
  collapsed badly, or when the user's instructions seem wrong. Also triggered by
  "/fable-team:judge" or "I'm stuck on a decision".
---

# /fable-team:judge — Launch the Judgment Playbook

The substance lives in the bundled `playbook.md` (single source of truth; never duplicated into SKILL.md).
Premise: **heuristics are not rules.** In situations that call for deviating, you may deviate — record the reason.

## Steps

1. **Read the bundled `playbook.md`** (in this repository:
   `${CLAUDE_PLUGIN_ROOT}/skills/judge/playbook.md`; it ships with the skill in plugin distribution too)
2. Find the heuristic that matches the decision you face, and apply it
3. General form when no heuristic matches:
   - If reversible, try it small. If irreversible, ask the user (with options + a recommendation)
   - If you lack the information needed to decide, it is an investigation problem, not a judgment
     problem (route to scout)
4. **Record the decision**: during mission work, leave "decision and reasoning" in journal.md (the Conductor appends directly).
   Write the rationale so a successor won't relitigate it. If you deviated from a heuristic, record why

## Rules

- Don't stall because you're unsure. If you still can't decide after running this playbook,
  it is a decision the user should make (batch your questions into a single ask)
- Don't carry major design decisions (high cost to reverse) alone — consult architect (Opus)
