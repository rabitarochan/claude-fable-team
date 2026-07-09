# Fable Team

[日本語 (Japanese)](README.ja.md)

A **Claude Code plugin** that recreates Fable 5's ability to carry long-running tasks
through to completion — in a world where Fable 5 has retired — via a **division of labor
among Opus / Sonnet / Haiku**.

The handoff document written by Fable 5 itself is in [HANDOFF.md](HANDOFF.md).

## Installation

```
# 1. Add the marketplace (or use a local path to this repository for a local trial)
/plugin marketplace add rabitarochan/claude-fable-team

# 2. Install the plugin
/plugin install fable-team@fable-team

# 3. Set up in the target project (creates the state directory + embeds the rules into CLAUDE.md)
/fable-team:init
```

## Updating

```
# 1. Refresh the marketplace metadata
/plugin marketplace update fable-team

# 2. Update the installed plugin
/plugin update fable-team@fable-team

# 3. Re-run init in each set-up project — needed only when the release notes say the
#    canonical rules (rules.md) changed. Idempotent: replaces only the section between
#    the fable-team markers in CLAUDE.md
/fable-team:init
```

Note: third-party marketplaces do not auto-update by default. Per-marketplace
auto-update can be enabled from the `/plugin` → Marketplaces tab.

## Quick Start

```
1. Set the main session to Opus            /model opus
2. One-shot task (single-session)          /fable-team:task fix <something>
3. Start a long-running mission            /fable-team:mission implement <something>
4. Run the execution loop                  /fable-team:work
   (to keep it running automatically)      /loop /fable-team:work
5. Session died, or it's the next day      /fable-team:resume in a new session
6. After the mission completes             /fable-team:retro to harvest insights
7. When signals have accumulated           /fable-team:grow to improve the team itself
```

One-shot tasks go to `task`; anything that spans sessions goes to `mission`.
When in doubt, ask "Will you continue this tomorrow?" **You can always promote; you can never demote.**

### Which permission mode to start in

Start in **normal mode** — Plan Mode is not needed as the session entry point.
The intake (`task` / `mission`) already carries its own "recon → plan → approval" gate
and persists the plan to `plan.md`, so stacking Plan Mode on top approves the same plan
twice; worse, Plan Mode blocks writing the `.fable-team/` state files that intake creates.
Once the plan is approved and the delegation loop is running, raising to auto-accept
edits fits well (it is close to a prerequisite for `/loop /fable-team:work`).
Plan Mode still earns its keep in two places: a major change of direction mid-mission,
and raw edits outside the framework where you want a hard no-edit guarantee.

## Structure

```
claude-fable-team/       ← The Claude Plugin itself (this repository)
├── .claude-plugin/
│   ├── plugin.json        Manifest
│   └── marketplace.json   Self-hosted marketplace definition
├── agents/              ← 7 specialist subagents
│   ├── architect.md       (Opus)   Design and planning
│   ├── debugger.md        (Opus)   Root-cause analysis of hard bugs
│   ├── reviewer.md        (Opus)   Adversarial code review
│   ├── builder.md         (Sonnet) Implementation and test writing
│   ├── verifier.md        (Sonnet) Behavior verification (E2E)
│   ├── scout.md           (Haiku)  Exploration and research (parallel fan-out)
│   └── scribe.md          (Haiku)  Checkpoints and recovery recording
├── skills/              ← 1 setup + 1 brainstorm + 1 one-shot + 5 mission + 4 playbook + 1 growth
│   ├── init/              Project setup (bundles rules.md, the canonical rules)
│   ├── brainstorm/        Pre-mission brainstorming: diverge, converge, draft goal/DoD for task/mission intake
│   ├── task/              One-shot task execution (single-session, with a promotion path)
│   ├── mission/           Mission kickoff (bundles templates/ and a filled-in example/)
│   ├── work/              Execution loop (delegate → verify → record, with unattended loop mode)
│   ├── checkpoint/        Freezing state
│   ├── resume/            Full recovery in a new session
│   ├── retro/             Harvesting insights after completion
│   ├── grow/              Growing the team itself (signal distillation → asset updates)
│   └── debug/ verify/ brief/ judge/   Playbook skills (each bundles a playbook.md)
├── README.md / HANDOFF.md / CHANGELOG.md / CLAUDE.md (for HQ)
└── .fable-team/         ← State of this HQ repository itself (not part of the distribution)
```

Only two things are added to a target project:
**`.fable-team/`** (mission state and the growth loop) and **`.claude/skills/pj-*/`** (harvested
project-specific skills; those usable across projects graduate to `~/.claude/skills/`).

## Design Philosophy (in one paragraph)

Fable 5's long-horizon consistency was achieved through "a single enormous context."
Fable Team replaces it with "disciplined state externalization into the `.fable-team/` directory."
The truth lives in files, not in context, and any session may die at any moment.
Work that needs judgment goes to Opus, volume production goes to Sonnet, breadth and speed go to Haiku,
and every deliverable counts as done only after passing "observable completion criteria" and behavior verification.

## Development (growing this repository)

- Changes to the framework require approval and are recorded in `CHANGELOG.md` with their evidence signals
- Verification procedure: `claude plugin validate .` → install locally →
  run through the full flow starting from `/fable-team:init` in a real project
- Commit at every checkpoint (the change history itself becomes the team's growth history)
