---
name: verify
description: >
  Apply the Fable Team verification playbook. Use when confirming that a code change actually
  works, judging whether a task's completion criteria are met, or running acceptance checks at a
  phase gate or before release, or right before delegating verification to verifier, or before
  delegating a test-writing task to builder (the playbook's "Test Design" section). Also use
  when "the tests pass but I want to confirm it really works". Also triggered by
  "/fable-team:verify" or "verify by the playbook".
---

# /fable-team:verify — Launch the Verification Playbook

The substance lives in the bundled `playbook.md` (single source of truth; never duplicated into SKILL.md).
Watchword: **Green tests ≠ working software.** Only what has been observed counts as verified.

## Steps

1. **Read the bundled `playbook.md`** (in this repository:
   `${CLAUDE_PLUGIN_ROOT}/skills/verify/playbook.md`; it ships with the skill in plugin distribution too)
2. **When delegating** (the default): to verifier. The brief must include —
   the observable completion criteria (write the expected results first) / the change type (API, CLI,
   config, migration, UI, etc.; the verifier uses it to pick a playbook recipe) /
   `${CLAUDE_PLUGIN_ROOT}/skills/verify/playbook.md` as a reference.
   When delegating a **test-writing** task to builder, include the same path in that brief and
   point at the playbook's "Test Design" section
3. **When verifying yourself**: follow the recipe for the relevant change type.
   Minimum set = 1 happy path + 1-2 representative error cases + 1 nearby regression check

## Rules

- Write the expected results **before executing**. Never look at the output first and then declare it "correct"
- Never accept — or give — an "I checked it" without evidence (the command + its actual output)
- Never blur "unverified" and "verified OK". Mark anything you could not observe as unverified, with the reason
- During mission work, reflect verification results in the "verification status" section of state.md (the Conductor edits directly)
