# Current state: <mission name>

> **This file is the single source of truth.** Any session may die at any moment.
> Update it after every task completion and every checkpoint.
> If this file and reality (code, test results) disagree, reality is the truth. Record it in the journal and fix this file.

- slug: `<slug>`
- Phase: Phase N — <name>
- Progress: X of Y tasks done
- Last updated: YYYY-MM-DD HH:MM (use the actual system time; do not guess)
- Updated by: <Conductor session / scribe>

## Next move (most important)

<!--
Quality bar: a session seeing this repository for the first time can resume work from this alone.
Include: target task number / target files / commands to run / expected results /
         if work is in progress, how far the last session got
-->

<Write it here>

## In progress / stopping point

<Work in progress and where in which file it stopped. If none, write "None">

## Verification status

<!-- Do not mix "verified" and "unverified". Only what verifier has observed counts as verified -->

- Verified: <what has actually been run and confirmed>
- Unverified: <what has not been observed yet>

## Blockers / notes

<Waiting on the user, environment issues, warnings from predecessors, etc. If none, write "None">
