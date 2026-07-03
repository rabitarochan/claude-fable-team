# Verification Playbook

> Primary readers: the verifier (Sonnet). Also used for the builder's self-verification.
> Conductor: when delegating verification tasks, include this file in the brief's "References".

## Common Principles

1. **Write the expected result before you run.** Never look at the output first and declare it correct after the fact
2. Minimum set: **1 happy path + 1–2 representative error paths + 1 regression check on nearby code that should not have changed**
3. **Keep evidence.** Include the commands you ran and the actual output (key parts) in the report. "Confirmed." on its own is not verification
4. Never mix "unverified" with "verified OK"

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

## When There Is No Verification Environment

- Build a minimal test harness in the scratchpad yourself (a few dozen lines is often enough)
- Anything you still cannot observe, return explicitly marked "unverified (reason)". Never mark OK what you cannot observe
