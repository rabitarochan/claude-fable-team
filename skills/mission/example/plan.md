# Execution plan: TODO management REST API

> Author: architect / Approved: 2026-06-29
> Status legend: ⬜ not started / 🔄 in progress / ✅ done (verified) / ⏸️ blocked

## Assumptions

- Node.js 22 is available locally
- Data volume is personal-use scale (SQLite is sufficient). If this breaks, replan starting from DB selection

## Key design decisions

| Decision | Choice | Rationale | Rejected alternatives |
|---|---|---|---|
| DB access | better-sqlite3 | Synchronous API keeps tests simple; sufficient for this scale | Prisma (overkill for a small project; deep dependency tree) |
| Auth method | API key (header) | The user explicitly said simple is fine | JWT (leans too far toward the out-of-scope full-fledged auth) |

## Phase 1: CRUD foundation

**Gate**: reviewer LGTM + actually start the app and observe the happy path of every endpoint via curl
→ **passed 2026-06-30** (see journal)

| # | Task | Owner | Completion criteria (observable) | Depends on | Status |
|---|--------|------|----------------------|------|------|
| 1.1 | Project scaffold (TS/Express/test setup) | builder | The sample test passes with `npm test`, and the app starts with `npm start` | - | ✅ |
| 1.2 | Implement todos CRUD | builder | POST/GET/PUT/DELETE behave per spec via curl | 1.1 | ✅ |
| 1.3 | Test coverage (all CRUD paths + error cases) | builder | `npm test` all green; stable under parallel runs (20 consecutive green runs) | 1.2 | ✅ |

## Phase 2: Authentication and user separation

**Gate**: reviewer LGTM + observe via curl that user A's key cannot touch user B's TODOs

| # | Task | Owner | Completion criteria (observable) | Depends on | Status |
|---|--------|------|----------------------|------|------|
| 2.1 | users table and API key issuance | builder | `POST /users` returns 201 + a key; includes the display_name column (changed 07-01, see journal) | - | ✅ |
| 2.2 | Auth middleware | builder | `npm test -- auth` all green; 401 for missing/invalid key | 2.1 | 🔄 |
| 2.3 | Per-user TODO separation | builder | GET on B's TODO with A's key → 404; nothing leaks into listings | 2.2 | ⬜ |
| 2.4 | README (startup steps, API list) | builder | Following the written steps as-is starts the app and every API responds | 2.3 | ⬜ |

## Risks

| Risk | Detection | If it materializes |
|---|---|---|
| better-sqlite3 build fails in this environment | At npm install during 1.1 | Swap in sql.js (architect re-decides) |
| Misreading what "simple auth" means | User confirmation at the Phase 2 gate | Update the Definition of Done in mission.md and replan |
