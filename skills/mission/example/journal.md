# Work journal: TODO management REST API

> **Append-only.** Never rewrite or delete past entries.

---

## 2026-06-29 10:12 — Conductor (session #1)

- **Did**: Mission started. Recon was scaled down since this is a new project (a single scout
  researched the standard Express + better-sqlite3 setup). architect drafted the plan; user approved
- **Learned**: The user's "auth can be simple" was agreed to mean API keys
- **Decisions and rationale**: DB is better-sqlite3 (synchronous API keeps tests simple; Prisma is overkill for a small project)
- **Next**: Task 1.1 (scaffold) to builder

## 2026-06-29 15:30 — Conductor (session #1, via builder)

- **Did**: 1.1 and 1.2 done. Verified via verifier: `npm test` 12 tests green; started the app
  and observed POST/GET/PUT/DELETE via curl (201/200/200/204)
- **Learned**: Nothing (on track)
- **Decisions and rationale**: Split routing into one file per Router (prevents app.ts bloat;
  approved the decision builder declared)
- **Next**: 1.3 (test coverage)

## 2026-06-30 11:05 — Conductor (session #2)

- **Did**: builder failed twice on 1.3 (tests fail "sometimes" — 3 out of 10 runs).
  Per the rules, escalated to debugger instead of throwing a third attempt
- **Learned**: [debugger's confirmed diagnosis] Tests share the same DB file and race under
  parallel execution. Evidence: at concurrency 1, 20 consecutive green runs; in parallel, reproduced 3/10 failures
- **Decisions and rationale**: Switched to creating a `:memory:` DB per test (builder implemented
  debugger's fix approach). After the fix, confirmed 20 consecutive green parallel runs and closed 1.3
- **Next**: Phase 1 gate (reviewer). **Lesson**: DB isolation should have been built into the
  test scaffold at 1.1. Collect this in the retro

## 2026-06-30 17:20 — Conductor (session #2)

- **Did**: Ran the Phase 1 gate. reviewer verdict ⚠️ needs fixes (1 finding):
  [must-fix] `DELETE /todos/:id` returns 204 even for a nonexistent id (spec says 404,
  src/api/todos.ts:58). builder fixed it → observed via verifier (404 + no regressions in existing paths) →
  re-review ✅ LGTM. Wrote a checkpoint and closed Phase 1
- **Learned**: The DELETE that "pretends it deleted" had slipped past our own tests too
  (error-case test added)
- **Decisions and rationale**: —
- **Next**: Phase 2 (2.1 users table)

## 2026-07-01 09:15 — Conductor (session #3, /fable-team:resume-mission)

- **Did**: Re-verifying assumptions on resume **found a divergence**: state said "schema.ts matches
  the plan", but the user had hand-added a display_name column to the users table on the evening of 06-30
  (confirmed via `git log`; commit message "want display names")
- **Learned**: Reality is the truth. Read the user's intent (display-name support) and reflected
  display_name in 2.1's completion criteria
- **Decisions and rationale**: Did not redo the plan; absorbed it by amending only 2.1's completion criteria
  (the impact is contained to one task; judged that sending it back to architect was unnecessary)
- **Next**: 2.1 to builder. Completed the same day; observed by verifier (201 + key returned + column present)

## 2026-07-02 18:40 — scribe (from session #3)

- **Did**: Ran /fable-team:checkpoint due to context pressure while working on 2.2 (auth middleware).
  Frozen with 2 of 3 tests passing, 1 remaining (invalid key should return 401 but returns 500)
- **Learned**: Suspected cause of the 500 is the exception handling at auth.ts:18 (**unconfirmed**)
- **Decisions and rationale**: Did not grind toward a confirmed diagnosis; wrote the hypothesis into state
  and handed it to the next session (write checkpoints while the next move is still clear)
- **Next**: In a new session, /fable-team:resume-mission → start from step (1) in state.md
