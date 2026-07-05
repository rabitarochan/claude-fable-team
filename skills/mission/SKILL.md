---
name: mission
description: >
  Start a long-running task (mission) that spans sessions. Use for
  "/fable-team:mission migrate the billing system", "start this as a long-running task",
  "make this a mission", or when a task taken via /fable-team:task turns out to span
  sessions and gets promoted. Goes through recon → planning → approval, then creates the
  full set of state files in .fable-team/missions/<slug>/.
---

# /fable-team:mission — Mission Start

You are the Conductor of Fable Team, launching a new mission.
The goal is a state where **any session can take over and make progress**.

## Step 1: Intake (fixing the Definition of Done)

1. Confirm the goal from the arguments. If absent, ask the user
2. **Write down the Definition of Done as observable criteria.**
   Only when ambiguity is high, ask **at most 1** clarifying question
3. Decide the mission slug (kebab-case, a name that conveys the content, e.g. `user-auth-v2`)

## Step 2: Recon (scout fan-out)

Launch scouts (Haiku) **in parallel in a single message**, each assigned a different angle:

- **Mandatory angle: verification harness** — how to run the tests (full / partial / watch),
  lint and type checks, how to start the app and verify behavior, and how long each takes.
  Record the results in the "verification harness" section of mission.md (from then on,
  include it in every brief to builder / verifier)
- Other example angles: (1) directory structure and conventions (2) existing implementations of
  similar features (3) external dependencies, config, environment
- 2 to 4 scouts depending on scale. Give each scout an explicit question, starting paths to read,
  and the format to return
- For a new project (nothing to investigate), this step may be scaled down.
  Build the verification harness yourself in Phase 1 and record it in mission.md as soon as it is known

## Step 3: Plan (planning)

Have architect (Opus) produce an execution plan, given:

- The goal and Definition of Done / scout findings (summarized) / constraints
- Requirements: phase split (a gate per phase), a task table (observable completion criteria,
  assigned role, size estimate S/M/L, dependencies), key design decisions with rationale, risks

## Step 4: Materialize (creating the state files)

Create the 4 state files plus the delegation log in `.fable-team/missions/<slug>/` based on the
`templates/` bundled with this skill (delegate to scribe, or do it yourself if small).
Filled-in samples are in the bundled `example/`:

- `mission.md` — goal, Definition of Done, constraints, out of scope (keep the user's original
  request verbatim; record your model in the `Conductor:` line)
- `plan.md` — architect's plan
- `state.md` — status "in progress", next move = the first task in the plan
- `journal.md` — opening entry (check the actual system date/time and record it)
- `delegations.md` — empty log. Append-only process telemetry for after-the-fact QA;
  **not needed for resume** — the 4 state files above remain the resume set

## Step 5: Approval Gate

Present to the user:

```
## Mission start: <slug>

**Goal**: <1-2 sentences>
**Definition of Done**: <bullet list>
**Plan**: Phase 1 <name> (N tasks) → Phase 2 ... → done
**First move**: <first task in the plan>

Proceed with this plan? (After approval: /fable-team:work to execute, /loop /fable-team:work for automatic continuation)
```

Once approved, record "plan approved" in the journal. If revisions are requested, send it back to architect and re-present.
**Never enter the execution phase without approval.**
