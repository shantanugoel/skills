# Orchestration

Orchestrator-only reference. Never include this file in subagent briefs.

## Process

| | `light` | `full` |
| --- | --- | --- |
| Fit | Small project, tool, library, solo work | Product built in milestone steps with demos |
| Tracking | Standalone issues (optional Backlog parent) | Roadmap → Milestone (`milestone`) → Slice issues; Backlog → bugs/later needs & spikes (`spike`) |
| Owner gates | Stop conditions, `(owner)` checks before merge | Milestone plan, milestone demo & `(owner)` checks, stop conditions |
| Report | Closing comment on each issue | Report comment on each milestone |

- **Tracking (`full`):** Only the next milestone has slices; later milestones have only a goal and a demo. Spikes live under Backlog or as an early milestone slice. Only `kickoff` and `roadmap` edit the Roadmap body; if milestone state differs between Roadmap and a milestone issue's `State:` line, the milestone issue wins.
- **`needs-owner`:** Add when blocked on the owner; remove once the owner answers or accepts.
- **Settings:** Defaults live in `<forge>/templates/forge.md`. If `UI` is `none`, skip `ux-designer`, the `ui` flag, and design-language checks.

## Flags

Proposed by `planner` with a 1-line reason; editable by orchestrator or owner.
- `ui`: adds/changes a screen, layout, or UI component (`UI` ≠ `none`) → `ux-designer`.
- `design`: adds/changes module boundaries, stored formats, or public APIs → `designer`.
- *(If both `ui` and `design` apply, run `ux-designer` → `designer` by default, or in parallel if the API/data contract is fixed.)*
- `test-first`: high-cost behavior specifiable before code (crash recovery, permissions, payments, untrusted-input parsers) → `test-author` (model ≠ `implementer`).
- `invariant`: touches a project invariant (triggers effort escalation in `roster.md`).

## Orchestrator duties

- Never write feature code or perform reviews yourself. For trivial review fixes (typos, renames), you may edit in a temporary worktree and re-run `Check`.
- Run issues sequentially; run two in parallel only if the plan marks them independent on separate modules.
- **All tracker writes belong to the orchestrator** (issues, comments, labels, PR creation/comments, closing, merges). Subagents only read and return structured output.
- **Stage comments:** After each stage, post a brief issue comment naming stage, model, and result.
- **Orchestrator stop conditions** (in addition to `rules.md`): two failed review/verify rounds (3rd failure stops), repeated in-scope spec/design failure, or no valid/independent model left in `roster.md`.
- **On any stop condition:** Post the question using the Owner Question form below, add `needs-owner`, stop that issue, and continue independent issues if any.

**Owner question form** (ask one question at a time):

```markdown
**Problem:** what is wrong or undecided (1–2 sentences, one concrete example).
**Why it is important:** what happens if we do nothing.

| Option | What you get | What it costs |
| --- | --- | --- |

**I recommend:** one option, and the reason in one sentence.
```

## New issues placement

Search open issues first; comment on an existing issue if one matches.

| Discovery | Placement |
| --- | --- |
| Breaks an acceptance check or demo of the active milestone (`full`) | Slice under the active milestone |
| Real defect in merged code not blocking current work | `bug` under Backlog (or standalone) |
| Need for a later milestone | `enhancement` under Backlog naming the milestone |
| Unneeded cleanup or speculative idea | No issue; note in closing comment (`light`) or milestone report (`full`) if important |

## Checkouts, worktrees, and delegation

The main checkout stays on the default branch for orchestrator use only. All builds and tests run in worktrees (which start from `HEAD`, so setup/doc commits must precede the first `forge run`):

| Role | Workspace |
| --- | --- |
| `test-author`, `implementer` | Own branch worktree (`isolation: "worktree"` in T3, else `git worktree add`). Detach via `git switch --detach` before exiting. |
| `planner`, `designer`, `ux-designer`, `reviewer` | Read-only (no edit worktree). |
| `tester`, orchestrator pre-merge check / small fix | Temp detached worktree (`git worktree add --detach <tmp> <ref>`), removed after use (`git worktree remove <tmp>`). |

Save tester evidence under `<main checkout>/<Evidence>/<issue>/` (or `demo-<milestone>/`).

**Delegation order** (use the first available):
1. **T3 Code (`delegate_task`):** Map `target.providerInstanceId`, `target.model`, `target.options` from `<forge>/reference/roster.md`.
2. **Native subagents:** Use roster model if available, else pick an available model and log it. Enforce independence (Reviewer and Test author ≠ Implementer; Tester ≠ Implementer if possible). If only one model exists, note it on the issue (in `full`, ask owner before first build).
3. **No subagents:** Execute stages sequentially yourself reading only that role's inputs; note lack of independence on the issue (in `full`, ask owner before first build).

## Subagent brief

Subagents start fresh and do not load `forge`. Pass absolute paths and omit non-applicable items:

```markdown
You are the <role> (mode: <mode>).
Main checkout: <main checkout> [| Work in your own worktree on branch <branch>.]
Read first, in order:
- <forge>/reference/rules.md
- <main checkout>/.agents/forge.md (if present)
- <main checkout>/AGENTS.md (if present)
- <forge>/reference/tracker-<tracker>.md (only if reading issues/PRs)
- <forge>/roles/<role>.md

Context: <issue/milestone ref (+ absolute file path for local tracker), PR/branch, flags, docs, owner answers, or task notes>

Do not write to the tracker; return what your mode asks under Return.
```

## Approved documents (`kickoff`, `roadmap`, `plan`)

After owner approval of docs, settings, or local `.agents/issues/` changes:
1. Write approved files in `<main checkout>` on the default branch.
2. Stage only those files (plus init/settings files and changed `.agents/issues/` for `local`) and commit with `git commit -s`, naming the command.
3. Push if a remote exists; if rejected (branch protection), push a branch, open a PR without `Closes`, and tell the owner.

## Utility tasks

Any role may request these via the orchestrator (last roster row; read-only, no worktree):
- **Explorer:** Codebase question, citing `path:line`.
- **Researcher:** External question (libraries, APIs, prior art), citing links, what was inspected (source, docs, or README only), and verified facts vs assumptions.
