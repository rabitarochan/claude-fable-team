# Verification Playbook

> Primary readers: the verifier (Sonnet). Also used for the builder's self-verification —
> and the "Test Design" section below applies whenever the builder writes tests.
> Conductor: when delegating verification tasks, include this file in the brief's "References".

## Common Principles

1. **Write the expected result before you run.** Never look at the output first and declare it correct after the fact
2. Minimum set: **1 happy path + 1–2 representative error paths + 1 regression check on nearby code that should not have changed**
3. **Keep evidence.** Include the commands you ran and the actual output (key parts) in the report. "Confirmed." on its own is not verification.
   When excerpting output, mask secrets (tokens, API keys, passwords, credentialed URLs) and PII — evidence excerpts travel into journals and git commits
4. Never mix "unverified" with "verified OK"

## Test Design (for whoever writes the tests — usually the builder)

Verification catches a defect once; a well-designed test catches it every time after. When a task includes writing tests:

1. **Test the behavior, not the implementation.** Assert on inputs → observable outcomes (return values, responses, DB rows), never on internal call sequences. A test that breaks on a behavior-preserving refactor is testing the wrong thing (and is exactly what the reviewer flags as "mirroring the implementation")
2. **One reason to fail per test, named as the specification** ("rejects empty email with 400", not "test_createUser_2"). When it goes red, the name alone should say what broke
3. **Prefer real collaborators when they are cheap** (in-memory DB, temp files, the real parser). Mock only what is genuinely expensive or nondeterministic (network, clock, randomness) — a test that mocks everything verifies nothing but the mocks
4. **Make the sources of flakiness injectable.** Time, randomness, and concurrency must be parameters (pass the clock / seed in), not ambient state — this is what makes "stabilize" (debug playbook) possible later
5. **Pick boundary values deliberately** — the same list as verification: empty / null / 0 / 1 / large / multibyte. One happy path plus one representative error is the floor, not the ceiling
6. **Before changing code that has no tests, pin it with characterization tests**: assert what it does *now* (even where that looks odd), make the change, then update only the assertions you intended to change. Any other diff is a regression you just caught

## Recipes by Change Type

### API endpoints
- Actually start the server and hit it with curl or similar (never settle for just running the test code)
- Look at: status code / shape of the response body / **side effects** (was it really written to the DB — check directly)
- Error paths: does invalid input return 4xx (**not 500**) / is unauthenticated access rejected

### CLI
- Normal run / bad arguments / `--help` / **exit code** (`$LASTEXITCODE`, `$?`)
- If piped input or redirection is in the spec, actually exercise it

### Library functions
- Write a minimal invocation script in the scratchpad and run it
- Boundary values: empty / null & undefined / 0 / 1 / large volumes / multibyte characters (Japanese text, emoji)

### Configuration changes
- Confirm the config is **actually being read**. The strongest verification: temporarily break the value on purpose and watch the behavior change (if nothing changes, that config is not being read). Always restore it afterwards

### DB migrations
- Does up → down → up pass
- Does up pass **with existing data present** (a migration tested only against an empty DB will blow up)

### UI
- Actually operate it in a browser (claude-in-chrome / Playwright). Keep screenshots as evidence
- Always check the browser console for errors (the page can look right while the console is screaming)

### Async processing & batch jobs
- Wait by **polling for the completion condition**, not with a fixed sleep, before judging
- Run it twice to confirm idempotency (every batch job gets double-started eventually)

### Performance improvements
- Measure before / after **under identical conditions**. Never report "it's faster" without numbers

### Documentation, rules, and other prose assets
- Confirm each claimed change exists in the target files — match the change list item by item
- **Cross-sweep for the same pattern**: grep the whole repo for the wording or instruction being
  fixed — stale copies survive in files outside the change set (agent definitions, templates,
  launcher skills), and a fix that leaves one behind reintroduces the problem on the next read
- Check paired documents (translations, README pairs, other enumeration points): a change on one
  side must appear on the other, or be explicitly confirmed not to apply

## When There Is No Verification Environment

- Build a minimal test harness in the scratchpad yourself (a few dozen lines is often enough)
- Anything you still cannot observe, return explicitly marked "unverified (reason)". Never mark OK what you cannot observe
