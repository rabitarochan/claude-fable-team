---
name: debug
description: >
  Apply the Fable Team debugging playbook. Use when starting on a bug investigation, an
  unexplained error, a flaky test (fails intermittently), or "it worked until yesterday" /
  "it behaves differently across environments" problems, or right before delegating debugging
  work to debugger / builder. Also triggered by "/fable-team:debug" or "debug by the playbook".
---

# /fable-team:debug — Launch the Debugging Playbook

The substance lives in the bundled `playbook.md` (single source of truth; never duplicated into SKILL.md).

## Steps

1. **Read the bundled `playbook.md`** (in this repository:
   `${CLAUDE_PLUGIN_ROOT}/skills/debug/playbook.md`; it ships with the skill in plugin distribution too)
2. **When delegating** (the default; see the CLAUDE.md routing table): to debugger (cause unknown, or after 2 failed attempts)
   or builder (a fix where you have a good guess at the cause). Always include
   `${CLAUDE_PLUGIN_ROOT}/skills/debug/playbook.md` in the brief's "references"
3. **When doing it yourself**: follow the playbook's standard procedure —
   reproduce → stabilize → isolate → hypotheses and discriminating conditions → minimal reproduction → fix → close the detection gap

## Rules

- Don't call a restated symptom a diagnosis. Only what **explains the mechanism and is consistent
  with the observations** counts as a diagnosis
- Even if a symptomatic fix makes the symptom disappear, report it as "unresolved" unless the mechanism is explained
- During mission work, record confirmed diagnoses and decisions in journal.md (the Conductor appends directly)
