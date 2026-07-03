# Briefing Playbook — The Art of Delegation

> Primary readers: the Conductor (main session).
> Most delegation failures come not from the agent's lack of ability but from missing information in the brief.

A subagent is a **zero-context stranger** who has seen none of your conversation and none of your prior thinking.
Write accordingly. The flip side: with a good brief, even Sonnet and Haiku will exceed your expectations.

## How to Write the Five Elements (the CLAUDE.md Delegation Rules)

1. **Background** — Why this task exists, in 1–2 sentences. Mission name and phase. Don't pass long history (reading cost degrades quality)
2. **Task** — Write it as a verb. **One delegation = one task.** No "and while you're at it..."
3. **Constraints** — State explicitly what must not be touched. Prohibitions cannot be guessed
4. **Deliverables** — Specify down to the format ("a list of implementation sites in `path:line` format")
5. **References** — **The Conductor names the files** to read. "Find and read the relevant files" adds exploration cost and drops both quality and speed

For implementation and verification briefs, include the "verification harness" section of mission.md
(test, lint, and launch commands) every time. Making the agent rediscover it throws away minutes on every delegation.

## Before / After Examples

### Delegating to a scout

❌ **Bad**: "Look into the auth stuff"
(Unclear what you want to know → reads everything indiscriminately and reports it all → the parent context overflows)

✅ **Good**:
> Question: Where is the login flow implemented, and how are sessions stored?
> Starting point: under `src/auth/`.
> Return format: `path:line` for each implementation site with a one-line description each; session storage mechanism as a one-sentence conclusion.
> No copies of file contents needed.

### Delegating to a builder

❌ **Bad**: "Build the user registration API"
(Style, completion criteria, and touchable scope all left to the agent → rework guaranteed)

✅ **Good**:
> Background: todo-api mission, Phase 2. We need a registration API to separate TODOs per user.
> Task: Implement `POST /users` (plan.md task 2.1).
> Constraints: Do not modify `src/db/schema.ts`. Match the structure and naming of the existing `src/api/todos.ts`.
> Completion criteria: `npm test -- users` passes. Empty email returns 400; valid input returns 201 with a Location header.
> References: `src/api/todos.ts` (style exemplar), `src/db/schema.ts` (users table definition).

## Acceptance Check on Returned Work

Check before integrating and reporting the returned results:

- [ ] Does it answer **each completion criterion, one by one** (send it back if it is just a "done" summary)
- [ ] Is verification **evidence** attached (commands + output)
- [ ] Does it declare "decisions I made on my own" (undeclared judgment calls are the scariest kind)
- [ ] For important tasks, **spot-check exactly one item** against the real thing yourself (inspecting everything is unnecessary; inspecting nothing is dangerous)

## How to Ask the User Questions

- Ask **once, in a batch**. Never drip questions one at a time (don't make the user pay for their time in installments)
- Attach **options plus a recommendation**. Ten times easier to answer than an open question, and the answers get better too
- Never ask what you can look up. Ask only what **only the user can know** (intent, priorities, preferences, internal context)
- Decide your own recommendation before asking. A question you cannot attach a recommendation to means you haven't researched enough
