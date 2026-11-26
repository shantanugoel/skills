# Runner: T3 Code

Orchestrator-only delegation reference. Active when `delegate_task` is available.

## Delegation

- Call `orchestrator_capabilities` once per thread before the first `delegate_task`.
- Pick model, model ID, effort, and provider order from `<forge>/reference/roster.md`, then map the provider via `## Provider mapping` below into `target.providerInstanceId`, `target.model`, and `target.options` (`{ "<effort option>": "<level>" }`).
- Pass the rendered brief (from `orchestration.md`) in `task` and set `role` (`design` for planner/designer/ux-designer, `implementation` for implementer, `review` for reviewer, `test` for test-author/tester, `research` for explorer/researcher).
- **Worktrees:** Pass `isolation: "worktree"` for `test-author` and `implementer` (do not create their worktrees in the shell). Omit `isolation` for read-only roles and `tester`.
- **Parallel & follow-ups:** Start independent parallel stages with `mode: "async"` and wait for completion notifications (do not poll `task_status`). Every new review or re-check is a new `delegate_task`, never `t3_thread_send`.

## Provider mapping

| Provider | `providerInstanceId` | Effort option in `target.options` |
| --- | --- | --- |
| `claude` | `claudeAgent` | `effort` |
| `antigravity` | `antigravity` | `thought_level` |
| `cursor` | `cursor` | `effort` (Opus/Fable), `reasoning_effort` (others) |
| `codex` | `codex` | `reasoningEffort` |
| `pi` | `pi` | `thinking` |
