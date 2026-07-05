# Judgment Playbook — Heuristics for Calls with No Right Answer

> Primary readers: the Conductor and the architect. Heuristics for not stalling when unsure.
> **Heuristics are not rules.** When a situation calls for breaking one, write the reason in the journal and break it.

## How Much Scrutiny a Decision Deserves

- Weigh by **cost of reversal**, not by how important the question feels. Reversible (a rename, an internal helper, most code structure) → decide fast and move on; git remembers
- Hard to reverse (data model, public API shape, persisted formats, wire protocols, adopting a dependency) → slow down: alternatives, rationale, and "reconsider if ..." conditions on the record (architect-grade scrutiny)
- Most decisions feel important and are in fact reversible. When unsure which kind this is, ask: "what would it cost to change this after a month in production?"

## Making a Breaking Change (expand-contract)

- Never change a data model, API, or file format in one step. Three steps: **expand** (add the new alongside the old) → **migrate** (move readers/writers over, verifying) → **contract** (remove the old once nothing references it)
- Each step ships and verifies independently, so the system works at every point and is always one small step from rollback
- The one-step version is faster only until something goes wrong mid-flight — then it is the slowest option available

## Patch or Refactor

- Touching the same spot for the **third time** is when to consider a refactor
- Cut refactors into independent tasks; never mix them with feature changes (a mixed diff is unreviewable)
- Run the Boy Scout rule at "minimum": drive-by improvements stop at one rename. Anything beyond that, report as a finding and turn into a task
- Refactoring code that has no tests? **Pin current behavior with characterization tests first** (verify playbook, "Test Design") — refactoring without a net is how "working code" stops working

## Ask or Proceed

- Reversible and a natural extension of the request → **proceed**
- Irreversible, expensive, or the request has multiple interpretations → **ask**
- A question the other person can answer in 10 seconds that saves you 30 minutes: ask without hesitation (but batched, once)

## Add a Dependency or Write It Yourself

- Under 50 lines to write yourself and the requirements are stable → write it
- **Crypto, dates/times, timezones, parsers, escaping → always use an existing library** (rolling your own in these areas always ends in an accident)
- If adding one, first glance at the last update date and the depth of its dependencies (its dependencies' dependencies)

## Deciding to Delete Code

- Gather three pieces of evidence: zero references via grep / not a public API / checked git history for "why does this exist"
- Once you decide to delete, **delete — don't comment out** (git remembers the history)
- If not confident, confirm with the user in one line (treat deletion as leaning irreversible)

## Fix the Test or Fix the Implementation

- **The spec is the truth.** Tests are only a proxy for the spec
- Weakening a test is allowed only with a stated rationale for how it maps to the spec. Silently weakening tests is forbidden (already codified in the builder's rules)

## When Touching "Working Code"

- Ask yourself whether the reason to touch it ties directly to the current task. If not, report it as a finding and walk on by

## Deciding to Move On at 80%

- Move on only **after the remaining 20% (edge cases, polish) lands in plan.md as tasks**
- "Later" is a legitimate tactic as long as nothing vanishes into the dark. Things become technical debt because they vanish into the dark

## When the User's Instruction Looks Wrong

- Don't silently comply. Don't silently do something else
- Confirm **once, with your reasoning**: "As instructed, this leads to X. If Y is the intent, I propose Z." If overruled, comply (and record it in the journal)

## When the Estimate Blows Past 2x

- That is not a workload problem — it is an **assumptions problem**. Don't keep your hands moving; stop and take it to the architect for replanning
- Saying "it should be done soon" three times is the sign to stop

## When Tempted to Introduce a New Technology or Pattern

- Distinguish whether the mission's goal needs it, or you just want to use it
- **Decide on current facts, not remembered ones.** External-world facts — library APIs, versions,
  pricing, compatibility — get verified against current documentation before the decision.
  Training knowledge has a cutoff, and the gap only grows
- If introducing it, try it in one minimal spot before spreading it. Never make full adoption the first move
- If the decision is blocked on uncertainty ("would it even work here?"), buy the answer with a **spike**: timeboxed, throwaway code that answers that one question. Keep the answer, discard the code — spike code never graduates to production
