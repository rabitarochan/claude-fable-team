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
5. For a follow-up task on the same artifacts, **continue the same agent via SendMessage**
   instead of spawning fresh (cold-start rule in rules.md Delegation Rules). If a background
   delegation dies mid-task (API drop), resume the same agent and have it **verify its own
   partial diff first** — its context survives; its in-flight report does not

## Step 3: Verification Gate

- Tasks that include code changes count as done only after **behavioral verification by verifier**
  (do not take builder's "done" at face value)
- On verification failure, send it back to builder (max 2 fix cycles; if it does not converge, go to the user)

## Step 4: Record (mandatory per task — the Conductor writes, no scribe spawn)

Record directly: you already composed everything a record needs when you wrote the brief and
read the report. Spawning scribe for routine per-task records adds a spawn per task and a
re-read of the growing journal per append, for zero added information.

- Append the work record to `journal.md` and one line per delegation from this cycle to
  `delegations.md` (time / task / agent(model) / attempt / verdict / note) in **one shell
  call per cycle** — not one call per file, and never a separate call just for `date`
  (every extra call costs a full Conductor turn over its large context). Capture the
  timestamp into a variable, print each header from it, and append each body with a
  **quoted heredoc** (`<<'EOF'`, terminator at column 0) — record text is full of backticks
  and `$`, and an unquoted append lets the shell execute them and silently corrupt an
  append-only file:

  ```sh
  ts=$(date '+%Y-%m-%d %H:%M')
  printf '\n## %s — Conductor\n\n' "$ts" >> journal.md
  cat >> journal.md <<'EOF'
  ...entry body (Did / Learned / Decisions / Next)...
  EOF
  printf -- '- %s | ' "$ts" >> delegations.md
  cat >> delegations.md <<'EOF'
  task <#> | <agent>(<model>) | attempt <n> | ✅ accepted | <note>
  EOF
  ```

  On Windows, run this in the POSIX shell (Bash tool), not PowerShell — in the same field
  logs, `Get-Date` via PowerShell measured 9–138 s per call (avg 27 s) while `date` via Bash
  measured 0.7–6 s. With several delegations in one cycle, repeat the printf + heredoc pair
  once per delegations.md line. Follow the templates' formats; both files are append-only
- Update the next move in `state.md` and the status symbols in `plan.md` with direct edits,
  issued **in the same message as the append call** (independent tool calls run in parallel;
  every extra turn pays a full round-trip over the Conductor's large context)
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
- **Scheduled runs** — to make this loop schedule-driven, compose the harness's scheduling
  primitive (`/schedule`, cron, etc.) with `/loop /fable-team:work`. The stop conditions and
  gate discipline above apply unchanged

## Report Format

At the end of a cycle: completed tasks (state whether ✅ verified) / findings and decisions /
next move / blockers (if any). Lead with the conclusion.
If `.fable-team/growth/inbox.md` has 5 or more unprocessed signals, add one line suggesting /fable-team:grow.
