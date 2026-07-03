---
name: task
description: >
  Execute a one-shot task (minutes to hours, done within a single session) with Fable Team's
  quality discipline — work that does not warrant a full mission. Use for
  "/fable-team:task fix the login bug", or whenever an implementation, bug fix, investigation,
  or refactoring request arrives that fits in one session. Also triggers on "delegate this to
  subagents", "run these in parallel", or "have the team do it".
  If it turns out mid-task to span sessions, promote to /fable-team:mission.
---

# /fable-team:task — One-Shot Task Execution

Design philosophy: **Skip the mission's heavy gear (the 4 state files). Never skip the quality
discipline (delegation, verification, honest reporting).** A small task is no excuse for sloppy work.

## Step 0: Weight-Class Triage (first 10 seconds)

| Class | Rule of thumb | Approach |
|---|---|---|
| **Light** | Small single-file fix, answering a question, a one-command investigation | The Conductor executes directly without delegating. Still never skip verification (Step 3) |
| **Medium** | Touches multiple files, has parallelizable independent work, needs investigation | Decompose → delegate (go to Step 1) |
| **Mission-class** | Spans sessions, exceeds several hours, multi-stage Definition of Done | Do not take it with this skill — go to `/fable-team:mission` |

When unsure, start lighter and promote when it breaks down. **You can always promote; you can never demote.**

## Step 1: Decomposition and Completion Criteria

- Decompose the task into **units that can run independently in parallel**
- Write **observable completion criteria** for each unit. If you cannot, you do not understand it well enough — send a scout first
- Present the plan upfront only when: it includes destructive operations / it involves public
  release / the request is open to multiple interpretations.
  Otherwise proceed without presenting one (an always-on approval gate is too heavy for a
  one-shot task. If it is reversible and a natural extension of the request, act — that is the Fable way)

## Step 2: Execution Loop

- Delegate per the routing table (CLAUDE.md): investigation → scout / implementation → builder /
  unknown cause → debugger. Briefs use the five elements + verification harness (the /fable-team:brief playbook)
- Delegate units with no dependencies **in parallel in a single message**. Use worktree isolation
  only when they modify files at the same time
- builder fails twice → diagnose with debugger before re-delegating.
  If the fix cycle does not converge within 2 rounds, ask the user to decide (same discipline as missions)

## Step 3: Verification Gate (never skip, regardless of task size)

- Code changes count as done only after passing the verifier's **behavioral verification**
  (Green tests ≠ working software.)
- Do not impose reviewer (Opus) on every task. Add it only when the change is large or touches
  critical areas (auth, payments, data deletion, public APIs)

## Step 4: Report and Wrap-Up

- **Lead with the conclusion**: what was done (state whether ✅ verified) / decisions made / open issues and concerns
- If there are growth signals (corrections, rework, surprises, friction, success patterns), add
  one line to `.fable-team/growth/inbox.md` — one-shot tasks feed the team's growth too
- If this is a git repository, suggest a commit to mark the milestone

## When to Promote (switching to /fable-team:mission)

Promote without clinging when any of these signs appear:

- The estimate blew past 2x (a problem of assumptions, not workload — judgment playbook)
- It is now certain the work will not finish within this session
- Completion criteria started multiplying mid-work (more than 3 "while we're at it" additions)

When promoting, carry the findings, decisions, and partial results so far into the `/fable-team:mission` intake (do not discard them).
