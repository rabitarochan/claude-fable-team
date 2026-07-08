---
name: retro
description: >
  Look back on a completed (or aborted) mission and harvest its lessons. Use when told
  "/fable-team:retro", "run a retrospective", or "capture what we learned from this mission",
  or right after a mission completes. Proposes SkDD Skill harvesting and saves learnings to memory.
---

# /fable-team:retro — Retrospective and Lesson Harvesting

A mission's value is twofold: the deliverable and **the lessons for next time**. Reliably collect the latter.
The team gets stronger with every mission — if it keeps records.

## Steps

1. **Identify the target mission** (from the argument, or the most recently completed one)

2. **Read journal.md in full** (retro is the one occasion where reading it all is allowed).
   If it is long, you may delegate a summary of the first half to a scout (Haiku)

3. **Extract lessons** — answer these questions:
   - What was duplicated effort (rework, redoing things, wasted investigation)?
   - Which decisions were right / wrong? (Judge by the information available at decision time, not hindsight)
   - Where did estimates diverge from reality? (check plan.md's Size column against the
     attempt counts in delegations.md)
   - Where did the tokens go? (if the harness provides `/usage`, snapshot the breakdown by
     skill/subagent into the retro notes — delegations.md deliberately has no token column,
     so this is the one place to look)
   - Are there **new pitfalls to add** to the pitfall catalog in HANDOFF.md?

   Merge any unprocessed signals for this mission from `.fable-team/growth/inbox.md` into the lessons here.

4. **Check the effectiveness of previous changes (close the loop)** — look at the team-asset changes
   recorded in the changelog (`.fable-team/growth/changelog.md`; framework changes in `CHANGELOG.md`)
   since the last retrospective, and evaluate against this mission:
   did each one work, get broken, or go unused?
   Route changes that did not work to the next step as candidates for rewriting or deletion.
   **Changing things isn't growth unless you check they worked.**

5. **Distill and apply** — for triaging lessons (the destination table), Skill harvesting (SkDD), the approval gate,
   application, and changelog recording, follow the steps in `/fable-team:grow` (scoped to this mission only)

6. **Close out**:
   - Update the status in `mission.md` to "completed" (or "aborted" + reason)
   - Append a retro entry to the journal
   - Propose moving the mission to `.fable-team/missions/_archive/<slug>/` (never delete history)

## Principles

- Don't hunt for culprits. Hunt for pitfalls (patterns)
- "I'll be careful next time" is not a lesson. It becomes a lesson only when it
  **lands in the system (conventions, templates, skills)**
