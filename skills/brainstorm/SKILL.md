---
name: brainstorm
description: >
  Pre-mission brainstorming for when the goal itself is still fuzzy — diverge into options,
  converge on a direction, and draft a goal/Definition of Done before intake. Use when "I have a
  vague idea", "not sure what to build yet", "help me think through this before starting", or the
  user wants to explore a problem space before committing to a task or mission. Sits upstream of
  /fable-team:task and /fable-team:mission intake — if the goal is already known, skip this. Also
  triggered by "/fable-team:brainstorm".
---

# /fable-team:brainstorm — Pre-Mission Ideation

Use this when the goal itself is fuzzy and needs divergence before intake. If the goal is already
known, do not run this — go straight to `/fable-team:task` or `/fable-team:mission`. Brainstorm
produces a **draft** goal/DoD; the intake of `/fable-team:task` or `/fable-team:mission` finalizes
it. Do not duplicate intake's job.

## Steps

1. **Problem framing** (with the user, in dialogue): what itch or opportunity is this, for whom,
   and what would success feel like? Do this in conversation — do not skip to solutions.
2. **Divergence**: generate options through distinct lenses (catalog below).
   - **Default**: Conductor-led dialogue with the user, walking a few lenses together
   - **Only when the solution space is wide**: fan out to **Opus-tier agents (architect)**, each
     briefed with a different lens — ideation is generative judgment work, not breadth search, so
     this is not a scout task. This reuses the HANDOFF.md §5 "Judge Panel" pattern: independent
     proposals from different priorities, with scoring and merging staying with the Conductor
   - No idea-killing during this step (see Rules)
3. **Convergence**: cluster the options, score them against the user's constraints, and pick a
   direction **with the user** — the user picks, the Conductor recommends
   - If the emerging choice contradicts a previously recorded position (growth-inbox note, journal
     decision), surface that objection before converging and record why it is overridden
4. **Drafting**: write a goal draft (1-2 sentences) and an **observable** Definition of Done draft
5. **Intake routing**: recommend `/fable-team:task` (single session) or `/fable-team:mission`
   (spans sessions), using the existing heuristic: "Will you continue this tomorrow?"

## Lens Catalog (starter kit, not a methodology)

Pick 2-4 that fit the problem; do not run all of them mechanically.

- **Minimal implementation** — what is the smallest thing that could work?
- **User value** — what matters most to whoever benefits from this?
- **Risk/failure-first** — what breaks first, and how do we hedge against it?
- **Extensibility** — which choice keeps future options open?
- **Contrarian/invert** — what if we did the opposite of the obvious approach?
- **Adjacent domain** — how does a different field solve a similar problem?

## Output: Brainstorm Summary

End every brainstorm with this block, handed to the user:

```
## Brainstorm Summary

**Problem framing**: <what itch/opportunity, for whom, what success feels like>
**Options explored**: <each option, including discarded ones and why>
**Converged direction**: <the direction chosen, and why>
**Goal draft**: <1-2 sentences>
**Definition of Done draft** (observable):
- <bullet>
- <bullet>
**Recommended intake route**: /fable-team:task | /fable-team:mission
```

This summary is **ephemeral by default** — no state files, no directories. Paste it directly into
`/fable-team:task` or `/fable-team:mission` intake. If the user wants to keep refining it across
sessions, that itself is a sign it should be promoted to a mission.

## Rules

- Talk with the user in **the user's language** — the framework's internals are English, the
  dialogue is not
- A brainstorm produces **drafts, not commitments**. Never start implementing from a brainstorm;
  always route through intake first
- Do not create state files or directories for a brainstorm
- Diverge before you judge — no idea-killing during divergence
- The user owns the converged choice; the Conductor recommends, it does not decide
