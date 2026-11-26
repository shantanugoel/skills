---
name: forge
description: "A workflow that takes work from an issue to a merged change with subagents for spec, design, build, review and test. Commands: kickoff, init, roadmap, file, run, plan, run-milestone. Use only when the owner explicitly invokes it, for example /forge, $forge, /skill:forge or \"forge run 12\". Do not use it for a request that does not name forge."
disable-model-invocation: true
---

# forge

Syntax: `forge <command> <arguments> [one-run overrides]` (e.g., `"reviewer on Opus for this run"`).
If no command or an unknown command is given, show this table and stop.

| Command | Purpose | File |
| --- | --- | --- |
| `kickoff <idea>` | Turn an idea into vision, architecture, design language (if UI), and first spikes/setup issue. Offers `git init` and `init`. | `commands/kickoff.md` |
| `init` | Explore the repo, ask unresolved questions, and write `.agents/forge.md` and a minimal project `AGENTS.md`. | `commands/init.md` |
| `roadmap <what changed>` | Create or update roadmap, milestones, spikes, and docs; apply spike answers or milestone reports. | `commands/roadmap.md` |
| `file <words>` | Turn a rough bug report or request into a well-formed issue without fixing it. | `commands/file.md` |
| `run <issue>` | Take one issue (or spike) from spec to merge (or closed answer). | `commands/run.md` |
| `plan <milestone>` | Draft a milestone plan and slice list, then stop for owner approval (`full` process only). | `commands/plan.md` |
| `run-milestone <milestone>` | Execute all slices of an approved milestone, run the demo and doc check, then stop for owner acceptance (`full` process only). | `commands/run-milestone.md` |

## Before every command

1. Resolve `<forge>` to the absolute path of the directory containing this file. All `<forge>/...` paths refer to it.
2. Except for `kickoff` and `init`, require `.agents/forge.md` in the repository root. If missing, tell the owner to run `forge init` and stop.
3. Read `<forge>/reference/rules.md`, `<forge>/reference/orchestration.md`, and the command file.
4. When `.agents/forge.md` exists (and the command uses the tracker or subagents), also read `.agents/forge.md`, `<forge>/reference/tracker-<tracker>.md`, and `<forge>/reference/roster.md`.
5. Apply roster overrides in order: `roster.md` < `.agents/forge.md` ("Roster changes") < one-run overrides from the owner's command.
