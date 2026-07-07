# Current state: TODO management REST API

> **This file is the single source of truth.** Any session may die at any moment.

- slug: `example-todo-api`
- Phase: Phase 2 — Authentication and user separation
- Progress: 4 of 7 tasks done
- Last updated: 2026-07-02 18:40
- Updated by: scribe (from Conductor session #3)

## Next move (most important)

Continue task 2.2 (auth middleware). `src/middleware/auth.ts` already exists, and
`npm test -- auth` passes 2 of 3 cases. The remaining failure is "returns 401 for an
invalid key" — it currently returns 500. Suspected cause: `src/middleware/auth.ts:18`
does not catch the DB-lookup exception and passes it to next(err) (unconfirmed; verify first).

Steps: (1) fix the above → (2) confirm `npm test -- auth` is all green → (3) wire the
middleware into `src/app.ts` (all routes except /users) → (4) observe via verifier with curl
(no key 401 / invalid key 401 / valid key 200) → (5) record (direct journal append + state update) and move to 2.3.
An example brief for builder is in the journal's 07-02 entry.

## In progress / stopping point

Only 2.2 above. No other files are mid-edit (`git status` confirmed clean).

## Verification status

- Verified: all Phase 1 CRUD paths (real launch + observed via curl, 06-30); key issuance in 2.1 (same)
- Unverified: everything around auth (one 2.2 test still failing); error cases for registration including the display_name column

## Blockers / notes

- None
- Note: the user hand-added the display_name column to the users table on 07-01
  (see journal 07-01). schema.ts differing from the original plan is expected.
