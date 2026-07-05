# Delegation log: TODO management REST API

> Append-only process telemetry for after-the-fact QA and mentoring — not needed for resume.
> Dossiers only for ⤴ escalations / non-convergence (masked per Boundary Hygiene).

## Log

- 2026-06-29 13:05 | task 1.1 | builder(sonnet) | attempt 1 | ✅ accepted | scaffold green: `npm test` and `npm start` observed
- 2026-06-29 15:10 | task 1.2 | builder(sonnet) | attempt 1 | ✅ accepted | all CRUD paths observed via curl by verifier (recap: journal 06-29 15:30)
- 2026-06-30 09:30 | task 1.3 | builder(sonnet) | attempt 1 | ❌ sent back | tests fail in 3 of 10 parallel runs
- 2026-06-30 10:20 | task 1.3 | builder(sonnet) | attempt 2 | ⤴ escalated | still flaky with the same approach — stopped per the two-failure rule

### Dossier: task 1.3 attempt 2 (2026-06-30 10:20)

**Brief (verbatim, masked):**
> Background: example-todo-api, Phase 1. Task 1.3 test stabilization, attempt 2 (attempt 1 came back flaky).
> Task: make `npm test` stable under parallel runs.
> Constraints: do not weaken or skip tests.
> Completion criteria: 20 consecutive green runs.
> References: `test/todos.test.ts`, `src/db.ts`. Harness: `npm test` (~15 s).

**Report (verbatim, masked):**
> Added retry waits around the flaky assertions; parallel runs still fail 3 of 10.
> Same approach has now failed twice — stopping per the two-failure rule.
> Observed: every failure involves two test workers writing `todo.db` at the same time.

- 2026-06-30 10:45 | task 1.3 | debugger(opus) | attempt 1 | ✅ accepted | root cause: tests share one DB file and race in parallel (concurrency 1 = 20/20 green); fix strategy returned
- 2026-06-30 11:00 | task 1.3 | builder(sonnet) | attempt 3 | ✅ accepted | `:memory:` DB per test; 20 consecutive green parallel runs (recap: journal 06-30 11:05)
- 2026-06-30 15:40 | phase 1 gate | reviewer(opus) | attempt 1 | ⚠️ needs fixes | must-fix 1 / recommended 0 / FYI 0 — `DELETE /todos/:id` returns 204 for a nonexistent id
- 2026-06-30 16:30 | phase 1 gate fix | builder(sonnet) | attempt 1 | ✅ accepted | DELETE now returns 404 + error-case test added; verifier: no regressions
- 2026-06-30 17:15 | phase 1 gate | reviewer(opus) | attempt 2 | ✅ LGTM | gate passed (recap: journal 06-30 17:20)
- 2026-07-01 10:40 | task 2.1 | builder(sonnet) | attempt 1 | ✅ accepted | `POST /users` 201 + key + display_name column observed (see journal 07-01)
