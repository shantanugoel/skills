# Orchestration

Orchestrator-only reference. Do not include this file in subagent briefs.

## Process

| | `light` | `full` |
| --- | --- | --- |
| Fit | Small project, tool, library, solo work | Product built in milestone steps with demos |
| Tracking | Standalone issues (optional Backlog parent) | Roadmap → Milestone (`milestone`) → Slice issues; Backlog → bugs/later needs & spikes (`spike`) |
| Commands | `kickoff`, `init`, `roadmap`, `file`, `run` | All commands |
| Owner gates | Stop conditions, `(owner)` checks before merge | Milestone plan, milestone demo & `(owner)` checks, stop conditions |
| Report | Closing comment on each issue | Report comment on each milestone |

- **Tracking rules (`full`):** Only the next milestone has slices; later milestones have only a goal and a demo. Spikes live under Backlog or as an early milestone slice. Only `kickoff` and `roadmap` edit the Roadmap body; if milestone state disagrees between Roadmap and a milestone issue's `State:` line, the milestone issue is authoritative.
- **`needs-owner` label:** Add when blocked on the owner; remove once the owner answers or accepts.
- **Settings:** `.agents/forge.md` defines all project settings; defaults live in `<forge>/templates/forge.md`. If `UI` is `none`, skip `ux-designer`, the `ui` flag, and design-language checks.

## Flags

Proposed by `planner` with a one-line reason; editable by orchestrator or owner.

- `ui`: adds or changes a screen, layout, or UI component (only when `UI` setting is not `none`). Runs `ux-designer`.
- `design`: adds or changes module boundaries, stored formats, or public APIs. Runs `designer`.
- *(When both `ui` and `design` apply, default order is `ux-designer` → `designer` so user flows/states inform interfaces; run in parallel if the API/data contract is already fixed.)*
- `test-first`: high-cost behavior specifiable before code (crash recovery, permissions, payments, untrusted-input parsers). Runs `test-author` on a model different from `implementer`. Implementer must not alter those tests without explaining why in the PR.
- `invariant`: touches a project invariant. Escalate effort by one step for build and review.

## Orchestrator duties

- Do not write feature code or perform reviews yourself. Orchestrate stages, brief subagents, verify results, and maintain the tracker.
- For trivial review fixes (typos, renames), you may edit the branch yourself in a temporary worktree, then re-run `Check`.
- Never trust a report blindly: run `Check` yourself in a temporary worktree and inspect the diff summary before merging.
- Run issues sequentially. Run two concurrently only if the plan marks them independent and touching separate modules.
- **Orchestrator owns all tracker writes** (issue creation/edits, comments, labels, PR creation/comments, closing, merging). Subagents may read from the tracker when needed, but always return text/proposals for the orchestrator to write.
- **Stage comments:** After each stage, post a brief comment on the issue naming the stage, model, and result.
- **Stop conditions:** Post the question (using `rules.md` "Owner question form"), add `needs-owner`, stop that issue, and continue independent issues if any.

## Checkouts and worktrees

The main checkout stays on the default branch and is used **only by the orchestrator** (tracker actions, merges, approved doc commits). All code and test execution happens in worktrees:

| Role | Workspace |
| --- | --- |
| `test-author`, `implementer` | Own worktree on the issue branch. With T3 `delegate_task`, pass `isolation: "worktree"`; otherwise create one via `git worktree add`. Before finishing, release the branch with `git switch --detach` so the next stage can check it out. |
| `planner`, `designer`, `ux-designer`, `reviewer` | No edit worktree (read-only). |
| `tester`, orchestrator pre-merge check / small fix | Temporary detached worktree (`git worktree add --detach <tmp> <ref>`), removed after use (`git worktree remove <tmp>`). |

Save all tester evidence under `<main checkout>/<Evidence>/<issue>/` (or `demo-<milestone>/`) so it survives worktree removal.

## Delegation

Use the first available mechanism:

1. **T3 Code (`delegate_task`):** Resolve `target.providerInstanceId`, `target.model`, and `target.options` from `<forge>/reference/roster.md`. Pass `isolation: "worktree"` for `test-author` and `implementer`.
2. **Native subagents:** Use the roster model if available; otherwise pick an available model and record it on the issue. Enforce model independence (Reviewer and Test author ≠ Implementer; Tester ≠ Implementer if possible). If only one model exists, note the lack of independence on the issue (in `full` process, ask owner before the first build).
3. **No subagents:** Execute each stage yourself in order, reading only that role's inputs, and note the lack of independence on the issue (in `full` process, ask owner before the first build).

## Subagent brief

Subagents start with empty history and do not load `forge`. Always pass absolute paths and omit items that do not apply:

```markdown
You are the <role> (mode: <mode>).
Main checkout: <main checkout> [| Work in your own worktree on branch <branch>.]
Read these files first, in order:
- <forge>/reference/rules.md
- <main checkout>/.agents/forge.md (if it exists)
- <main checkout>/AGENTS.md (if it exists)
- <forge>/reference/tracker-<tracker>.md (only if the task reads issues/PRs)
- <forge>/roles/<role>.md

Context:
- <Issue/milestone ref (and absolute file path for local tracker), PR/branch, flags, docs, or owner answers>
- <Task-specific notes: fix findings, spike flag, focus, etc.>

Do not write to the tracker; return what the role's mode asks under Return.
```

## Approved documents (`kickoff`, `roadmap`, `plan`)

After the owner approves document or tracker-file changes on the default branch:

1. Write approved files in the main checkout on the default branch.
2. Stage only those files, any init/settings files created or updated, and changed `.agents/issues/` files (`local` tracker). Commit with `git commit -s`, naming the command in the commit message.
3. If a remote exists, push. If the push is rejected (branch protection), push a branch, open a PR with no `Closes` line, and inform the owner.

## Utility tasks

Any role may request these from the orchestrator (uses the last roster row; read-only, no worktree):

- **Explorer:** Answer a question about this repository, citing `path:line`.
- **Researcher:** Answer an external question (libraries, APIs, prior art), citing links, what was inspected (source, docs, or README only), and separating verified facts from assumptions.
