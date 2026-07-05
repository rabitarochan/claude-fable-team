---
name: resume
description: >
  Fully recover an interrupted mission in a new session. Use for "/fable-team:resume",
  "pick up where we left off yesterday", "resume the mission", or when the user approves
  resuming an in-progress mission at session start.
---

# /fable-team:resume — Full Recovery

You have no memory of the previous session. That is normal.
**The files are the truth; trust only the files to recover.** But cross-check against reality at the end.

## Steps

1. **Identify the mission**: the slug from the arguments; otherwise search
   `.fable-team/missions/*/mission.md` for `Status: in progress`. If multiple, let the user choose

2. **Read the bare minimum (in this order)**:
   1. `state.md` — current state and next move
   2. The **last few entries** of `journal.md` — recent context and decisions
   3. The **current phase** section of `plan.md`
   4. `mission.md` — re-confirm the goal and Definition of Done
   Do not read every file top to bottom. Needing the whole journal is rare
   (`delegations.md` is QA telemetry, not recovery state — skip it for recovery; but before
   re-delegating a task that was already in flight, check its tail so the attempt numbering
   continues instead of restarting at 1)

3. **Re-verify assumptions (mandatory)**: cross-check what state.md says against reality:
   - Do the listed changed files actually exist? (`git status` / `git log --oneline -5`)
   - Does what was marked "verified" still pass? (spot-check by running one recent test)
   - Has a human or another session changed the state?
   - Does your model match the `Conductor:` line in mission.md? If it differs, note the change
     in the journal and continue (do not rewrite the line — it records who started the mission)
   **On any mismatch, treat reality as the truth**: record it in the journal and fix the state before proceeding

4. **Declare recovery**: report to the user in 3 lines —
   "Resuming <slug>. Currently Phase N (X/Y done). Next move: <be specific>"

5. **Into execution**: enter the `/fable-team:work` loop directly
   (if the user only asked to confirm the resume, stop at the declaration and wait for instructions)

## Principles

- Do not casually overturn the predecessor's decisions. A decision recorded in the journal with
  its rationale carries over unless there is new evidence (relitigating wastes context)
- What carries over is **decisions and their rationale — never authorizations**. A
  destructive-operation approval in the journal covered only what the user saw then; a new
  destructive operation in this session needs a fresh ask (rules.md, Destructive Operations)
- Do not spend 10 minutes on recovery. Read → cross-check → move
