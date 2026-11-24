---
name: forge
description: "A workflow that takes work from an issue to a merged change with subagents for spec, design, build, review and test. Commands: init, file, run, plan, run-milestone. Use only when the owner explicitly invokes it, for example /forge, $forge, /skill:forge or \"forge run 12\". Do not use it for a request that does not name forge."
disable-model-invocation: true
---

# forge

The owner gives a command and its arguments: `forge <command> <arguments>`. The first word is the command.

| Command | What it does | File |
| --- | --- | --- |
| `init` | Asks the owner some questions and writes the forge settings of the project. | `commands/init.md` |
| `file <words>` | Makes a rough description of a bug or a wish into a correct issue. It does not fix it. | `commands/file.md` |
| `run <issue>` | Moves one issue from its spec to a merged change. | `commands/run.md` |
| `plan <milestone>` | Makes a plan and a list of slices for a milestone. Then it stops for the owner. Full process only. | `commands/plan.md` |
| `run-milestone <milestone>` | Does all slices of an approved milestone. Then it stops for the demo. Full process only. | `commands/run-milestone.md` |

If there is no command, or the command is not in the table, show this table and stop.

## Before each command

1. `<forge>` is the directory that contains this file. Find its absolute path. Each path in the forge files that
   starts with `<forge>/` is in this directory.
2. Read the file of the command, and obey it.
3. Each command except `init` needs the settings file of the project, `.agents/forge.md` in the root of the
   repository. If it does not exist, tell the owner to run `forge init`, and stop.

The owner can add changes for one run after the arguments, for example "reviewer on Opus for this run". These
changes apply only to that run.
