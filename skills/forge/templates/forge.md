# forge settings

Single source of truth for project settings. Edit directly, or re-run `forge init` for guided updates. Missing settings fall back to the defaults below.

## Settings

| Setting | Value (default) | Meaning |
| --- | --- | --- |
| Process | `light` | `light` (issues only) or `full` (roadmap, milestones, slices, demos) |
| Tracker | `github` | `github` (`gh` issues/PRs) or `local` (`.agents/issues/` + branches) |
| Repository | `checkout` | GitHub only: `owner/name` if issues live in another repo (e.g., upstream of a fork); `checkout` uses this repo |
| Check | `none` | Single merge-gate command for format, lint, and tests (`none` only until setup issue adds it) |
| Run | `README.md` | How a tester starts and exercises the real program (or public API for a library) |
| Evidence | `.evidence/` | Git-ignored directory for tester screenshots and logs |
| UI | `none` | Path to the design-language doc (e.g., `docs/design-language.md`) if the project has screens, else `none` |
| Browser | `agent-browser` | Browser tool for web UI verification (`agent-browser`, or the agent's browser tool; unused when `UI` is `none`) |
| Roadmap | `none` | Roadmap issue reference (`full` process only) |
| Backlog | `none` | Backlog issue reference (optional in `light`) |
| Branch | `issue/<issue>-<short-name>` | Work branch naming pattern |
| Docs | `README.md` | Docs or folders to keep accurate (e.g., `docs/architecture/`; one per line or comma-separated) |
| Dependencies | `Allowed. Give the reason in the pull request.` | Policy for adding new dependencies |
| Models | `Tests make no paid model call.` | Policy for LLM/model calls in tests and live runs |
| Released | `yes` | `no` deletes obsolete code freely; `yes` keeps compatibility unless the issue says otherwise |

## Invariants

Rules no change may weaken without owner approval. Write `none` if there are none.

- none

## Roster changes

Project-specific overrides to `<forge>/reference/roster.md`. Write `none` to use defaults.

- none
