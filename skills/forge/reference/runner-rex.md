# Runner: Rex

Orchestrator-only delegation reference. Active when `$REX_SESSION` is set, or when the owner requests Rex and `rex` is available. Runs each subagent CLI non-interactively in a Rex tab so progress stays visible.

## Delegation

- **Session:** Use `-s "$REX_SESSION"`. If unset, create one with `rex new forge -c "<main checkout>" --json` and use its `.session_id`.
- **Brief & output:** Write the rendered brief to a temp file (`$brief`) and capture output to `$out` (via `tee "$out"` with `set -o pipefail`, or the CLI's output flag) to avoid quoting issues and scrollback truncation.
- **Worktrees:** For `test-author` and `implementer`, create a detached worktree (`wt=$(mktemp -d)` then `git -C "<main checkout>" worktree add --detach "$wt" HEAD`), run with `-c "$wt"`, and remove it after the subagent detaches and exits (`git -C "<main checkout>" worktree remove "$wt"`). Read-only roles and `tester` run with `-c "<main checkout>"`.
- **Run & wait:**
  - Sequential: `rex run -s "$REX_SESSION" -c "$workdir" --label "forge-<role>" --focus=false --keep-open --json --wait -- sh -c '<cli cmd>'`
  - Parallel: omit `--wait`, save each `.block_ids[0]`, and wait with `rex wait -s "$REX_SESSION" "$block_id"`.
  - Read `$out` (or `rex capture -s "$REX_SESSION" -b "$block_id" --trim --unwrap` if needed), close finished blocks (`rex block close -s "$REX_SESSION" "$block_id"`), and remove temp files.

## Provider mapping

Pick model, model ID, effort, and provider order from `<forge>/reference/roster.md`. Skip any CLI not on `PATH` (or unauthenticated) and fall back per `roster.md`.

| Provider | Non-interactive CLI command | Read-only / Write flags |
| --- | --- | --- |
| `claude` | `claude -p --model <id> --effort <level> --no-session-persistence < "$brief"` | Read-only: `--permission-mode plan` (or `--allowed-tools` if running `git`/`gh`) · Write/test: `--permission-mode bypassPermissions` |
| `antigravity` | `agy -p --model <id> --effort <level> < "$brief"` | Read-only: `--mode plan` · Write/test: `--mode auto` (or `--dangerously-skip-permissions`) |
| `cursor` | `cursor-agent -p --trust --workspace "$workdir" --model '<id>[effort=<level>]' "$(cat "$brief")"` | Read-only: `--mode plan` · Write/test: `--force` |
| `codex` | `codex exec -m <id> -c model_reasoning_effort=<level> --ephemeral -C "$workdir" -o "$out" - < "$brief"` | Read-only: `-s read-only` · Write/test: `-s workspace-write --add-dir "<main checkout>/.git"` (or `-s danger-full-access` if tests need network/browser) |
| `pi` | `pi -p --no-session --model <id> --thinking <level> -- "$(cat "$brief")"` | Read-only: `--tools read,grep,find,ls` (add `bash` if reading `git`/`gh`) · Write/test: default tools |
