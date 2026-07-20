---
name: checkpoint
description: >
  Freeze the state of an in-progress mission right now. Use for "/fable-team:checkpoint",
  "save what we have so far", "let's stop here for today", "I want to switch sessions",
  or when the Conductor itself judges that the context is getting long.
---

# /fable-team:checkpoint — Freezing State

Create a state from which the next session can fully resume even if this session dies this instant.
**Take a checkpoint not "at a good stopping point" but "while the next move is still clear".**

## Steps

1. **Identify the target mission** (from the arguments, or the one in progress)

2. **Inventory the in-flight state**:
   - Tasks in progress and the exact interruption point (which file, how far)
   - Uncommitted changes (check with `git status` / `git diff --stat`)
   - What is verified / what is not (never mix them)
   - Decisions and findings that exist only in this context (these evaporate first)

3. **Delegate to scribe to record**:
   - A checkpoint entry in `journal.md` (with the actual system date/time)
   - Fully update `state.md`. Make the "next move" concrete enough for a first-time session to act on:
     target files, commands to run, expected results, how far the previous session got
   - Align the task status symbols in `plan.md` with reality

4. **Physical checkpoint**: if this is a git repository, suggest a WIP commit
   (commit the mission files together with it — including `delegations.md`)

5. **Self-test (mandatory)**: re-read state.md and ask yourself —
   **"Could an Opus session seeing this repository for the first time resume from this alone?"**
   If not, add what is missing before declaring completion.

## Report Format

```
## Checkpoint complete: <slug>

- Progress: Phase N — X of Y tasks done
- Frozen state: <1-2 sentences>
- How to resume: run /fable-team:resume-mission <slug> in a new session
```
