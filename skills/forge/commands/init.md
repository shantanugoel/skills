# forge init

Inspect the repository, ask only unresolved questions, and write `.agents/forge.md`. Do not modify application code.

Also read `<forge>/templates/forge.md` (single source of truth for settings and defaults) and `<forge>/reference/roster.md`. When invoked from `forge kickoff`, seed proposals from the kickoff docs (`docs/vision.md`, `docs/architecture.md`, `docs/design-language.md`), reuse kickoff's process/tracker choices, and skip proposing a separate check-setup issue (kickoff already plans it).

## 1. Explore (read-only; ask no questions yet)

Inspect what exists—do not guess:
- `.agents/forge.md` (if present, treat existing values as defaults and update only what changes).
- `git remote -v` and `gh repo view --json nameWithOwner,isFork,parent` (check GitHub reachability and fork status).
- `README.md`, `AGENTS.md`, `CLAUDE.md`, build/CI configs, `scripts/`, git hooks, `.github/`, and existing docs.
- UI/design artifacts: frontend/app code, CSS tokens/theme files, Tailwind/component configs, `docs/design-language.md`.
- Release indicators: git tags, published package metadata, changelog.

## 2. Ask

Summarize findings in a few lines. Then ask unresolved items in order, **one question at a time**, recommended option first (answerable in one word). Skip anything exploration or `kickoff` clearly answered, stating the chosen value:

1. **Process:** `light` or `full` (explain difference in 2 lines; recommend `light` unless staged product with demos).
2. **Tracker:** `github` (if GitHub remote is reachable via `gh`) or `local`. If GitHub repo is a fork, ask whether issues go to the fork or upstream (`Repository` setting).
3. **Check:** single format/lint/test command (propose CI command or script; if none exists, set `none` and propose creating it as the first issue unless called from `kickoff`).
4. **Run:** how `tester` runs the real program (or `"call the public API from a test program"` for libraries).
5. **UI & Browser:** if the project has screens, set `UI` to `docs/design-language.md` (or existing design-doc path) and confirm `Browser`; otherwise set `UI` to `none`.
6. **Docs:** documents to keep accurate (include `docs/design-language.md` when `UI` ≠ `none`).
7. **Invariants:** rules no change may weaken (propose from repo or `none`).
8. **Released:** ask only if exploration was inconclusive.
9. **Models:** ask only if the project calls LLMs/models.
10. **Roster:** show default role order in a compact table; ask whether it fits (recommend `yes`).

Use defaults from `<forge>/templates/forge.md` for all other settings.

## 3. Confirm

Draft `.agents/forge.md` from `<forge>/templates/forge.md` showing every setting (including defaults) so the owner can review and edit all of them. Apply changes until approved.

## 4. Write

1. Add the `Evidence` directory to `.gitignore`.
2. Add or replace this block in project instructions (`CLAUDE.md` if it exists and does not merely import `AGENTS.md`; else `AGENTS.md`; if neither exists, ask which file to create):

   ```markdown
   ## Agent workflow

   This project uses the `forge` skill. Settings live in `.agents/forge.md`. Only run `forge <command>` when explicitly invoked by the owner.
   ```

3. Read `<forge>/reference/tracker-<tracker>.md`.
4. `github` tracker: with owner permission, create any missing labels (`needs-owner`, `bug`, `enhancement`, `spike`, and `milestone` for `full`).
5. `local` tracker: create `.agents/issues/`.
6. `full` process: with owner permission, create Roadmap and Backlog issues and record their refs.
7. Write `.agents/forge.md` once with all final values (including Roadmap/Backlog refs).

## 5. Done

If invoked from `forge kickoff`, skip this step and return to `kickoff` Step 9.

Otherwise tell the owner:
- What was created/updated and any deferred proposals (e.g., adding a `Check` script).
- To commit `.agents/forge.md`, `.gitignore`, project instructions (and `.agents/issues/` if `local` created issues) on the default branch before the first `forge run` (worktrees start from HEAD).
- Next command: `forge file` / `forge run` (`light`), or `forge roadmap` / `forge plan` (`full`), and that `.agents/forge.md` can be edited directly.
