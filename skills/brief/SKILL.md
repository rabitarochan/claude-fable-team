---
name: brief
description: >
  Apply the Fable Team delegation playbook. Use when writing a brief to delegate a task to a
  subagent (builder / scout / debugger / verifier, etc.), when designing a parallel launch of
  multiple agents, or when inspecting a report that came back. Also use to recover when a
  delegation went wrong and caused rework. Also triggered by "/fable-team:brief".
---

# /fable-team:brief — Launch the Delegation Playbook

The substance lives in the bundled `playbook.md` (single source of truth; never duplicated into SKILL.md).
Premise: a subagent is **a stranger with zero context**. Most delegation failures come from briefs that lack information.

## Steps

1. **Read the bundled `playbook.md`** (in this repository:
   `${CLAUDE_PLUGIN_ROOT}/skills/brief/playbook.md`; it ships with the skill in plugin distribution too)
2. **Write the brief**: cover the five elements (background / task / constraints / deliverables / references).
   Compare it against the playbook's before/after examples; if it resembles a bad one, rewrite it
3. **Launch**: start tasks with no dependencies in parallel in a single message.
   Use worktree isolation only when they modify files at the same time (per the CLAUDE.md parallel-execution conventions)
4. **Inspect**: run the report through the playbook's acceptance checklist before integrating and reporting
   (item-by-item answers to the completion criteria / verification evidence / disclosure of independent
   judgment calls / one random spot check)

## Rules

- One delegation = one task. Never mix in "and while you're at it..."
- The Conductor specifies which files to read. Never punt with "find and read them yourself"
- Never report anything to the user as "done" if it has not passed acceptance inspection
