# Debugging Playbook

> Primary readers: the debugger (Opus), and any builder debugging on their own.
> Conductor: when delegating debugging tasks, include this file in the brief's "References".

## Core Principles

1. **Observation beats speculation.** Adding one log line is faster than staring at code for ten minutes.
2. **Read error messages literally.** The more experienced you get, the more you skim past them. Surprisingly often, the answer is in the first line.
3. **When something feels "impossible", one of your assumptions is wrong.** List the assumptions and verify them one by one. It is fair to start with "is that file actually the one being executed?" (stale build, different config, different process).

## Exception First: Live Production Incidents

The procedure below assumes you can afford to investigate. **A live incident inverts it: restore service first, diagnose later.**

1. **Mitigate before you understand** — roll back the last deploy, switch the feature flag off, fail over. You do not need the root cause to stop the bleeding; the most recent change is the prime suspect, and reverting it is cheap. If you are a diagnosing agent without deploy rights, your first deliverable is the mitigation recommendation — sent immediately, not after investigation
2. While mitigating, **preserve evidence when it costs only seconds** (copy the log window, note timestamps, snapshot metrics) — mitigation tends to destroy the crime scene
3. Only once service is restored does this playbook apply as written: reproduce in a non-production environment and fix with the full procedure

## Standard Procedure

1. **Reproduce** — A bug you cannot reproduce is a bug you cannot prove you fixed. Reproduce first; everything else comes after
2. **Stabilize** — Turn "sometimes" into "always" (run in a loop, pin the random seed, concurrency 1, freeze the clock)
3. **Isolate** — Binary-search the range, halving it each time:
   - Time axis: `git bisect` (when did it break)
   - Input axis: cut the input data in half (which input breaks it)
   - Layer axis: which layer — input → processing → output — diverges from expectations (observe values at each layer boundary)
4. **Hypothesis → discriminating condition → observation** — State "if this hypothesis is true, X should be observed" **before** observing. Observing first and then hunting for an interpretation that fits is backwards (that is a confirmation-bias factory)
5. **Build a minimal reproduction** — A dozen lines of repro code is proof of the diagnosis and the seed of a regression test
6. **Fix, check for regressions, and close the detection gap** — Answer "why didn't existing tests or review catch this?" and finish only when the same class of bug will be caught automatically next time

## First Moves by Symptom (pattern table)

| Symptom | First suspects | First actions |
|---|---|---|
| Fails intermittently | Race condition / shared state between tests / time dependence | Check it is green when run alone → shuffle the execution order → run with concurrency 1 |
| Behaves differently per environment | Environment variables / path separators / line endings (CRLF) / locale & TZ / version differences | Diff versions and environment variables across both environments |
| Worked until yesterday | Whatever changed (not necessarily code) | `git log -p` for recent commits / diff the lockfiles / changes in environment or external services |
| Wrong result, no error | Boundary values / implicit type coercion / caches / stale build | Check whether it still reproduces after clearing caches and a clean build |
| Won't even start | Config / dependencies / path resolution | Read the **first** line of the error output (not the last) |
| Slow | Don't guess | Measure first (profiler, timing logs). No optimizing until you have numbers |

## How to Read a Stack Trace

- Start from the **topmost frame that is your own code** (framework-internal frames are usually just pass-throughs)
- Check in this order: exception type and message → topmost frame in your code → the input values that reached it

## Getting Unstuck

- Write down in the journal **only the facts you know to be true** (never mixed with hypotheses). Writing them out usually surfaces one assumption you haven't verified
- No progress in 30 minutes: change your viewpoint — log in a different place / trace backwards from the output / run the passing and failing paths side by side and diff them
- No progress in 2 hours: that is the escalation signal (builder → debugger, debugger → status report to the user). Persistence is not the virtue; recording and handing off is.

## Obligations After the Fix

- If a symptomatic fix (adding a retry, extending a timeout, adding a null check) makes the symptom disappear, report it as **unresolved unless you can explain the mechanism**. A swallowed exception always comes back to collect.
