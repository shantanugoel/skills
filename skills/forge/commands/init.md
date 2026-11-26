# forge init

Inspect the repository, ask only unresolved questions, and write `.agents/forge.md` and a minimal, project-specific `AGENTS.md` (or update existing project instructions). Do not modify application code. Also read `<forge>/templates/forge.md`.

When invoked from `forge kickoff`, seed proposals from kickoff docs (`docs/vision.md`, `docs/architecture.md`, `docs/design-language.md`), reuse kickoff's process/tracker choices, and skip proposing a separate check-setup issue.

## 1. Explore (read-only; ask no questions yet)

Inspect what exists—do not guess:
- `.agents/forge.md` (if present, use existing values as defaults).
- `git remote -v` and `gh repo view --json nameWithOwner,isFork,parent`.
- `README.md`, `AGENTS.md`, `CLAUDE.md`, build/CI configs, `scripts/`, git hooks, `.github/`, and docs.
- UI/design artifacts: frontend/app code, CSS tokens/theme files, Tailwind/component configs, `docs/design-language.md`.
- Release signs: tags, published package metadata, changelog.

## 2. Ask

Summarize findings in a few lines, then ask unresolved items in order, **one question at a time** (recommended option first, answerable in one word). Skip clearly answered items while stating chosen values; use `<forge>/templates/forge.md` defaults for everything else:

1. **Process:** `light` vs `full` (per `orchestration.md`; recommend `light` unless staged product with demos).
2. **Tracker:** `github` (if reachable via `gh`) or `local`. If a GitHub fork, ask whether issues go to fork or upstream (`Repository`).
3. **Check:** CI command or script; if none, set `none` and propose adding it as the first issue (unless invoked from `kickoff`).
4. **Run:** start command for real E2E testing (or public API test call for libraries).
5. **UI & Browser:** if screens exist, set `UI` (e.g., `docs/design-language.md`) and confirm `Browser`; else `UI: none`.
6. **Docs:** docs to keep accurate (include `UI` doc when set).
7. **Invariants:** propose from repo or `none`.
8. **Released:** ask only if exploration was inconclusive.
9. **Models:** ask only if the project calls models.
10. **Roster:** show default role order in a compact table; confirm `yes` or record overrides.

## 3. Confirm

Draft `.agents/forge.md` from `<forge>/templates/forge.md` showing every setting (including defaults) and the proposed `AGENTS.md` (or `CLAUDE.md`) content/update. Apply edits until approved.

## 4. Write

1. Add `Evidence` directory to `.gitignore`.
2. Write or update `CLAUDE.md` (if present and not merely importing `AGENTS.md`), else `AGENTS.md` (default to `AGENTS.md` if neither exists, unless the owner prefers `CLAUDE.md`):
   - Keep it minimal and project-specific (seeded from kickoff docs and Step 1 findings; omit empty items and never duplicate `.agents/forge.md` settings): one-line purpose, links to `Docs`/`UI` doc, stack & key layout, build/check/run commands (or note that the setup issue adds them), and non-obvious project conventions/invariants. Preserve existing custom content when updating.
   - Add or replace this block:

   ```markdown
   ## Agent workflow

   This project uses the `forge` skill. Settings live in `.agents/forge.md`. Only run `forge <command>` when explicitly invoked by the owner.
   ```

3. Read `<forge>/reference/tracker-<tracker>.md`.
4. `github`: with owner permission, create missing labels (`needs-owner`, `bug`, `enhancement`, `spike`, plus `milestone` for `full`).
5. `local`: create `.agents/issues/`.
6. `full`: with owner permission, create Roadmap and Backlog issues and record their refs.
7. Write `.agents/forge.md` once with all final values.

## 5. Done

If invoked from `forge kickoff`, skip and return to `kickoff` Step 9.

Otherwise tell the owner: what was created/deferred, to commit `.agents/forge.md`, `.gitignore`, project instructions (and `.agents/issues/` if `local` created issues) on the default branch before the first `forge run`, the next command (`forge file`/`run` for `light`, `forge roadmap`/`plan` for `full`), and that `.agents/forge.md` is directly editable.
