# Skills

Agent skills that I use in my projects. They work with Claude Code, Codex, pi, OpenCode and other agents that read
skills.

| Skill | What it does |
| --- | --- |
| [forge](skills/forge/SKILL.md) | Takes work from an issue to a merged change. An orchestrator gives each stage (spec, design, UX/UI, build, review, test) to a subagent, which can use a different model. |

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
| `forge kickoff <idea>` | Turns an idea into `docs/vision.md`, `docs/architecture.md`, `docs/design-language.md` (if UI), and the first spikes. Does research, asks questions one at a time, and offers `git init` and `forge init`. |
| `forge init` | Explores the repo, asks unresolved questions, and writes `.agents/forge.md`. Run once per repository. |
| `forge roadmap <what changed>` | Creates or changes the roadmap, milestones, spikes, and docs. Applies spike answers or milestone reports. With no arguments, audits what is out of date. |
| `forge file <words>` | Turns a rough description of a bug or wish into a well-formed issue without fixing it. |
| `forge run <issue>` | Moves one issue (or spike) from its spec to a merged change (or closed answer). |
| `forge plan <milestone>` | Makes a plan and a list of slices for a milestone. Full process only. |
| `forge run-milestone <milestone>` | Runs all slices of an approved milestone, then runs the demo and stops for acceptance. Full process only. |

For a new idea, start with `forge kickoff`. Run the spikes that it creates with `forge run`. Then use `forge roadmap`
to apply their answers and make the milestones firm.

How you type the command depends on the agent: `/forge run 12` in Claude Code, `$forge run 12` in Codex,
`/skill:forge run 12` in pi.

### Settings

`forge init` writes `.agents/forge.md` in the repository. Edit it directly. Key settings:

- **Process.** `light` for a small project (issues and docs, no milestones). `full` for a product built in steps
  (roadmap, milestones with demos, and slices).
- **Tracker.** `github` uses GitHub issues and pull requests through `gh`. `local` stores issues as Markdown files in
  `.agents/issues/` and uses branches in place of pull requests.
- **Check.** One command that checks format, lint and tests. It is the merge gate.
- **UI.** Path to `docs/design-language.md` for projects with screens, or `none` (which skips the UX/UI designer and
  `ui` flag completely).

### Models

`skills/forge/reference/roster.md` maps each role to its preferred models, effort levels, and provider order. Projects
override it under `Roster changes` in `.agents/forge.md`, or per run via command arguments. Runner-specific delegation
and provider mappings live in `runner-t3code.md` (T3 Code `delegate_task`) and `runner-rex.md` (Rex terminal panes
running agent CLIs). Without either, forge falls back to the agent's native subagents or runs stages itself.

### Files

```
skills/forge/
├── SKILL.md       commands and bootstrap
├── commands/      one procedure file per command
├── reference/     rules (shared), orchestration (orchestrator-only), roster, runners, trackers
├── roles/         planner, designer, ux-designer, test-author, implementer, reviewer, tester
└── templates/     settings, issue/spike forms, vision, architecture, design-language
```
