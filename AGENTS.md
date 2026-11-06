# AGENTS.md — Open Group (organization)

This file is the global rule set for every repository in the `My-Clone-AI` organization (Open Group / Grupo Open). Each repo also has its own `AGENTS.md` for local startup, commands, and owners. The repo file wins on local paths and commands; this file wins on invariants.

Keep this file short. Put long guides in the owning repo and leave a pointer here.

OpenClaw Controller / NSVX lives here (`openclaw`, `clone`, and related apps). Follow each repo’s own AGENTS.md (OpenClaw’s root file must stay under 20,000 characters).

## What every Open Group agent does

1. Initialize before writing code: read `PROGRESS.md` or `.agents/harness/PROGRESS.md`, `DECISIONS.md`, `feature_list.json` if present, and `git log --oneline -5`. Record the exact HEAD sha. Run `./init.sh` or `.agents/harness/init.sh` when present.
2. Work on one feature at a time (WIP=1).
3. Do not mark a feature done because code was added. Done means verification evidence is recorded.
4. Leave a clean handoff: update progress, decisions, verification notes, and the feature list; delete leftovers (debug logs, temp files, commented-out code, stray TODOs).
5. If init verification fails, fix the baseline before any new feature work.

## Definition of done

Feature complete = end-to-end verification passed, not “code is written.”

1. Unit tests pass.
2. Integration tests pass.
3. End-to-end flow verification passes.

Do not start level 2 if level 1 failed. Do not start level 3 if level 2 failed.

## Diagnostic loop

A failure is a harness defect, not “the model being dumb again.” Name the layer, fix it, and do not fail that way again:

- task_specification
- context_provision
- execution_environment
- verification_feedback
- state_management

Append one JSON line per task to `.agents/harness/diagnostics/log.jsonl` (or `diagnostics/log.jsonl`): task, ok, layer (if failed), detail, fix.

## Golden rules

- Prefer the shared utility package over hand-rolled helpers.
- Do not YOLO-guess data structures. Validate boundaries or use typed SDKs.
- Prefer durable repo files over chat summaries.
- The implementer does not grade itself.
- UI: minimal, visuals over text, common words (show, hide, edit, save, list, progress). Official logos, not generic icons, when a brand exists.
- No Cursor, no CloudAgent, no Origin. Code lands through the Group Open pipeline (Master Grow: Codex, Muse, Claude) as PRs onto `develop`.
- Agent-native by default (AgentOS directive). Do not lift `clone_session` or owner sessions into plugins or the gateway.
- OpenClaw DEV gateway is `:18790`. Do not touch `:18789`.
- Do not mix Open Group / Grupo Open product surfaces with Universe branding. Follow each app’s product rules (including adult vs SFW separation).

## Loops

- `/goal` = one big task, runs until an independent checker says it is done (or max turns).
- `/loop` = one small action, repeats on an interval.
- Grow Ideas/Jobs = goal-based. Grow Timers = time-based. PR/CI hooks = event-driven.

## Cleanup

Before ending a session: startup path still works, verification still runs, progress is honest, no half-finished step is undocumented, next session can run without a manual repair.
