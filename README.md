# Skills

Agent skills that I use in my projects. They work with Claude Code, Codex, pi, OpenCode and other agents that read
skills.

| Skill | What it does |
| --- | --- |
| [forge](skills/forge/SKILL.md) | Takes work from an issue to a merged change. An orchestrator gives each stage (spec, design, build, review, test) to a subagent, which can use a different model. |

## Install

Install all skills for your user, for the agents that you use:

```bash
npx skills@latest add shantanugoel/skills -g -a claude-code -a codex -a pi -a opencode
```

The command puts the skills in `~/.agents/skills/` and links them into the directory of each agent.

Update them:

```bash
npx skills@latest update -g
```

To install one skill only, add `-s <skill>`.

## forge

forge does not start by itself. Start it with a command:

| Command | What it does |
| --- | --- |
| `forge init` | Asks some questions and writes the settings of the project to `.agents/forge.md`. Run it one time in each repository. |
| `forge file <words>` | Makes a rough description of a bug or a wish into a correct issue. |
| `forge run <issue>` | Moves one issue from its spec to a merged change. |
| `forge plan <milestone>` | Makes a plan and a list of slices for a milestone. Full process only. |
| `forge run-milestone <milestone>` | Does all slices of an approved milestone, then stops for the demo. Full process only. |

How you type the command depends on the agent: `/forge run 12` in Claude Code, `$forge run 12` in Codex,
`/skill:forge run 12` in pi.

### Settings

`forge init` writes `.agents/forge.md` in the repository. Edit it directly. The most important settings are:

- **Process.** `light` for a small project: issues only, with `file` and `run`. `full` for a product that grows in
  steps: a roadmap, milestones with a demo, and slices.
- **Tracker.** `github` uses GitHub issues and pull requests through `gh`. `local` keeps issues as Markdown files in
  `.agents/issues/` and uses branches in place of pull requests.
- **Check.** One command that checks format, lint and tests. It is the merge gate.

### Models

`skills/forge/reference/roster.md` tells which model does which role, and the providers in order. A project can
change it in the "Roster changes" section of its settings. With T3 Code, the orchestrator uses
`delegate_task` to start each subagent on its provider. Without it, forge uses the subagents of the agent, or does
the stages itself.

### Files

```
skills/forge/
├── SKILL.md       the commands
├── commands/      one file for each command
├── reference/     the workflow, the rules, the roster, the trackers
├── roles/         planner, designer, test author, implementer, reviewer, tester
└── templates/     the settings file that forge init starts from
```
