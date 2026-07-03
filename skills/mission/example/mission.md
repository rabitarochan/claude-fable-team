# Mission: TODO management REST API

- slug: `example-todo-api`
- Start date: 2026-06-29
- Status: in progress
- The user's request (verbatim):
  > Build a REST API for managing TODOs. I want each user's TODOs kept separate. Auth can be simple, but do write proper tests

## Goal

Build a TODO management REST API with Express + SQLite, with TODOs separated per user.
Authentication uses API keys (the user explicitly said simple is fine).

## Definition of Done

- [x] `npm test` passes in full (in a clean, CI-equivalent environment)
- [ ] It is observable via curl that API key auth blocks all access to other users' TODOs
- [ ] The README lists the startup steps and the API endpoints, and following those steps actually starts the app

## Verification harness (this project's feedback loop)

| Check | Command | Approx. duration |
|---|---|---|
| Tests (full) | `npm test` | ~15 s |
| Tests (partial) | `npm test -- <pattern>` | a few seconds |
| Lint / type check | `npm run lint && npm run typecheck` | ~10 s |
| Launch & smoke check | `npm start` → `curl localhost:3000/todos` | starts in ~2 s |

## Constraints

- Minimal dependencies (the user's preference; adding a framework requires discussion)
- Node.js 22 / TypeScript

## Out of scope

- Frontend
- Full-fledged auth such as OAuth ("maybe later" — per the user)
- Deployment / hosting
