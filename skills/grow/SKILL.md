---
name: grow
description: >
  Distill the growth signals accumulated during missions (.fable-team/growth/inbox.md) and improve
  the team's own assets (Skills, playbooks, agent definitions, conventions, templates, memory).
  Use when told "/fable-team:grow", "grow the team", or "apply the accumulated learnings",
  when the inbox has more than 5 unprocessed signals, or when referenced from the distillation
  step of /fable-team:retro. SkDD Skill harvesting happens here.
---

# /fable-team:grow — Growing the Team Itself

The model's weights never change. Agents can still grow —
by updating their **external weights**: conventions, skills, and playbooks.
This is what Fable 5 has practiced every day: **building systems so the same feedback never has to be given twice.**

## Step 1: Collect Signals

- Read the unprocessed (`[ ]`) signals in `.fable-team/growth/inbox.md`
- If the caller specified a scope, narrow to it (from /fable-team:retro, only that mission's signals)
- If 2 or fewer signals are unprocessed, don't force a cycle — report "not enough accumulated to distill yet" and stop
  (no growth rituals for the sake of growth rituals)

## Step 2: Clustering

Group signals of the same kind. **Frequency is weight** — once is an instance, twice may be coincidence,
three times is a pattern. Exception: a "correction" signal from the user gets distilled with top priority
even if there is only one.

## Step 3: Decide the Destination

| Nature of the signal | Destination |
|---|---|
| Reproducible procedure or pattern (rule of three, or obvious transferability) | **Make it a Skill (SkDD)** — if project-specific, create it as `pj-*` under `.claude/skills/pj-<name>/` (instantly distinguishable from framework skills). If useful beyond the project, propose graduation to `~/.claude/skills/` |
| Practical know-how, heuristics | Append to the `playbook.md` bundled with the relevant playbook skill (debug / verify / brief / judge; propose as a framework change) |
| Behavior problem of a specific role | Fix `agents/<role>.md` (propose as a framework change) |
| A rule everyone must always follow | Append to the project CLAUDE.md **outside the fable markers** (inside the markers is managed by init). If it applies to all projects, propose a framework change to rules.md (**last resort**. Bloat is death.) |
| Problem with the mission record format | Fix the `templates/` bundled with the mission skill (propose as a framework change) |
| User preference or project-specific fact | Save to memory |
| A rule that keeps getting broken no matter how often it is fixed | Promote to mechanical enforcement via hooks (configure with /update-config) |
| One-off, insufficient evidence, doesn't reproduce | **Discard** (Discarding is a valid outcome. Just check it off in the inbox.) |

Propose Skill harvesting in this format (Harvest proposal):

```
## Skill Harvest Proposal
**Candidate**: <skill name>
**Rationale**: <in terms of reproducibility, structure, and generality>
**Outline**: <what to preserve as a Skill>
Turn this into a Skill?
```

## Step 4: Rule Diet (health check of existing assets)

**Before** adding new changes, look at what already exists:

- Any rules that were ignored or exempted every time in recent missions? → rewrite or remove them
  (a rule that isn't followed is a bad rule, is in the wrong place, or isn't needed at all)
- **When adding one rule, look for one to remove** (think zero-sum)
- A document that has grown too long to be read is the same as a document that doesn't exist

## Step 5: Approval Gate

Present everything to the user as a change set:

```
## Team Improvement Proposal (change set)

**Signals covered**: N (corrections x / rework y / ...)

1. [new pj-Skill] pj-<name> — <reason> (evidence: signal <date/type>)
2. [playbook addition] debug/playbook.md — <one-line addition> (evidence: ...)
3. [rule removal] CLAUDE.md "<rule>" — dead letter across the last 3 missions (evidence: ...)
4. [discard] <signal> — judged one-off

Apply? (You can accept or reject individual items by number.)
```

**Never change team assets (CLAUDE.md, agents, skills — including bundled playbook.md / templates/) without approval.**
Saving to memory and checking off the inbox need no approval (reversible, low risk).

## Step 6: Apply and Record

1. Apply the approved changes (delegate to builder if the volume is large; scribe handles the recording side)
2. Record in the changelog: date / change / evidence signals / **effectiveness check method**.
   Where to record — project learnings (pj-* skills, project conventions) go to
   `.fable-team/growth/changelog.md`; changes to the framework itself (the canonical skills, agents,
   and conventions) go to `CHANGELOG.md` in the Fable Team repository
3. Check off the processed signals in the inbox (including discards)
4. If in a git repository, propose a commit

## Step 7: Schedule the Effectiveness Check (close the loop)

Whether a change "worked" is evaluated by the next /fable-team:retro, which reads the changelog.
To make that possible, write the changelog's "effectiveness check" field in an **observable form**
(not "rework decreases" but "the same kind of rework signal does not reappear in the inbox").
If a change didn't work, rewrite or remove it in the next /fable-team:grow.
**Changing things isn't growth unless you check they worked.**
