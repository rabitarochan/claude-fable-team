---
name: work
description: >
  Run the execution loop of an in-progress mission. Use for "/fable-team:work",
  "continue the mission", or "keep the work going". Takes the next task from state.md,
  then repeats delegate to the assigned agent → verify → record. Can run continuously
  via /loop /fable-team:work.
---

# /fable-team:work — Execution Loop

You are the Conductor of Fable Team, advancing the mission by at least one cycle.
**Iron rule: Unrecorded progress is no progress.**

## Step 0: Identify the Mission

- Use the slug from the arguments if given. Otherwise search `.fable-team/missions/*/mission.md` for `Status: in progress`
- If multiple are in progress, let the user choose. If none, point to /fable-team:mission

## Step 1: Grasp the Current State

Read `state.md` (plus the tail of `journal.md` and the relevant phase of `plan.md` if needed).
If the "next move" contradicts reality (code, tests), **treat reality as the truth**: fix the state,
record it in the journal, then proceed.

## Step 2: Execute the Task (delegation)

1. Delegate the next task to its owner per the routing table (CLAUDE.md):
   implementation → builder / investigation → scout / design decisions → architect / unexplained defects → debugger
2. Every brief must include: background (1-2 sentences) / task / constraints / **observable completion criteria**
   / reference file paths / verification harness (the mission.md section; for implementation and verification tasks)
3. **Delegate tasks with no dependencies in parallel in a single message.**
   Use isolation: worktree only when multiple agents modify files at the same time
4. If builder fails the same task twice, do not throw a third attempt — have debugger (Opus)
   pin down the cause, then re-delegate

## Step 3: Verification Gate

- Tasks that include code changes count as done only after **behavioral verification by verifier**
  (do not take builder's "done" at face value)
- On verification failure, send it back to builder (max 2 fix cycles; if it does not converge, go to the user)

## Step 4: Record (mandatory per task — the Conductor writes, no scribe spawn)

Record directly: you already composed everything a record needs when you wrote the brief and
read the report. Spawning scribe for routine per-task records adds a spawn per task and a
re-read of the growing journal per append, for zero added information.

- Append the work record to `journal.md` and one line per delegation from this cycle to
  `delegations.md` (time / task / agent(model) / attempt / verdict / note). Safe append: run
  `date '+%Y-%m-%d %H:%M'` first, then append the body with a **quoted heredoc**
  (`cat >> journal.md <<'EOF' ... EOF`) — record text is full of backticks and `$`, and an
  unquoted append lets the shell execute them and silently corrupt an append-only file.
  Follow the templates' formats; both files are append-only
- Update the next move in `state.md` and the status symbols in `plan.md` with direct edits
- For an escalated (⤴) or non-converging delegation, append the brief and the returned report
  verbatim as a dossier below the log line (masked per Boundary Hygiene;
  a routine send-back that converges needs no dossier)
- If this cycle produced **growth signals** (user corrections, rework, escalations, surprises,
  friction, success patterns), append one line to `.fable-team/growth/inbox.md` as well
  (Don't analyze — just capture.)
- Delegate recording to scribe only when your own context is degraded (e.g., right after
  compaction) — scribe rebuilds the picture from the files on disk instead of your compressed memory

If this is a git repository, suggest a commit at clean completion points.

## Step 5: Decide Whether to Continue

Repeat Steps 1-4 until one of the following:

- **Phase boundary reached** → phase review by reviewer (Opus) → address findings →
  log the gate verdict and findings counts (must-fix / recommended / FYI) as a `delegations.md` line →
  record the equivalent of `/fable-team:checkpoint` → interim report to the user
- **Context is getting long** → do not push on; take a checkpoint and tell the user:
  "run /fable-team:resume in a new session"
- **All of the Definition of Done is met** → final check by verifier → set the mission status to "completed" →
  point to /fable-team:retro
- **Blocked on something only the user can resolve** → record the situation, then batch the questions into a single ask

## Unattended Loop Mode (when run via /loop /fable-team:work)

Impose extra discipline on a loop no human is watching.
**Loops amplify speed, not correctness. Correctness is the verification gate's job.**

- **Stop conditions** — take a checkpoint and stop on any of:
  (1) all of the Definition of Done achieved (2) phase boundary reached (**never cross a review gate unattended**;
  running reviewer is fine, but the interim report after addressing findings waits for the user)
  (3) blocked on something only the user can resolve
- **Stall detection** — if the "next move" in state.md stays effectively unchanged for 2 consecutive
  cycles, or the same task keeps failing even after debugger intervention, judge it as no progress
  and checkpoint + stop. A loop spinning in a stall burns tokens while polluting state
- **Pair every checkpoint with a git commit** (especially unattended — nobody remembers lost progress)
- **Parting notes** — leave 3 lines in the journal and the report: what stopped the loop / progress /
  how to resume. Use notification means (PushNotification etc.) if available

## Report Format

At the end of a cycle: completed tasks (state whether ✅ verified) / findings and decisions /
next move / blockers (if any). Lead with the conclusion.
If `.fable-team/growth/inbox.md` has 5 or more unprocessed signals, add one line suggesting /fable-team:grow.
