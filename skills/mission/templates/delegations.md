# Delegation log: <mission name>

> **Append-only process telemetry for after-the-fact QA and mentoring — not needed for resume.**
> (state.md remains the single source of truth for recovery; never read this file to resume.)
> One line per delegation, appended at the end in chronological order.
> Timestamps come from the Conductor — run `date` first, then append the entry with a quoted heredoc
> (`<<'EOF'`) so the shell never interprets body text; when recording is delegated to scribe
> (checkpoints), the brief passes the timestamp (scribe cannot check the clock). Never guess a time.
> **Dossier rule**: only when a delegation escalates (⤴) or a fix cycle does not converge,
> append the brief and the returned report verbatim right below the log line — masked per
> Boundary Hygiene (no secrets / PII; this file is committed with checkpoints).
> A routine ❌ send-back that then converges needs no dossier (the metric line is enough).

Line format:

`- YYYY-MM-DD HH:MM | task <#> | <agent>(<model>) | attempt <n> | ✅ accepted / ❌ sent back / ⤴ escalated | <one-line note>`

- `attempt <n>` counts delegations of the same task to the same role. The fix-cycle count is the
  highest attempt number — no separate counter
- Reviewer gates at phase boundaries use the same line format, with findings counts in the note.
  Gate lines carry the reviewer's own verdict vocabulary (✅ LGTM / ⚠️ needs fixes / ❌ reimplement):
  `- YYYY-MM-DD HH:MM | phase N gate | reviewer(opus) | attempt 1 | ⚠️ needs fixes | must-fix 1 / recommended 2 / FYI 0`

Dossier format (⤴ / non-convergence only):

### Dossier: task <#> attempt <n> (YYYY-MM-DD HH:MM)

**Brief (verbatim, masked):**
> ...

**Report (verbatim, masked):**
> ...

## Log

<!-- append below this line -->
