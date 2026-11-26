# forge run <issue>

Take one issue (or spike) from spec to merged change (or closed answer).

## 1. Read issue and check for spike

Read `<issue>` first.

**If labeled `spike`**, run only these stages and stop:
1. **Spec:** `planner` (`Spike`)—or refine yourself if already crisp—and update the issue body.
2. **Experiment:** `implementer` (`Spike`) in a worktree (or `researcher` without a worktree if no code is needed). Post the returned `Spike answer` on the issue. *(Time-box exhaustion with partial findings is a valid result, not a failure.)*
3. **Review:** `reviewer` (`Spike`); post comment. On `changes-needed`, loop back to `implementer`/`researcher` (max 2 fix rounds).
4. **Close:** delete experiment branch (local + remote if pushed) and close issue. For standalone spikes, tell owner to run `forge roadmap` (`run-milestone` handles milestone spikes).

## 2. Preconditions (regular issues)

Verify before starting (if any fails, inform owner and stop):
- Slice has an approved milestone plan; standalone issue fits one PR (else advise splitting in `light` or a milestone in `full`).
- Every issue under `Needs` is closed.
- Default branch passes `Check` (skip if `Check` is `none` or this issue adds `Check`).

## 3. Stages

1. **Spec:** `planner` (`Issue`), or write yourself for a small issue (`templates/issue.md`). Confirm checks are observable and in scope, then update issue body.
2. **Design (by flag, per `orchestration.md`):** `ux-designer` (`Screen design`) for `ui` (when `UI` ≠ `none`); `designer` (`Issue or milestone design`) for `design`. Write or update the `## UX/UI design` / `## Design` section(s) in the issue body.
3. **Tests first (`test-first`):** `test-author` in its own worktree; post handoff comment noting `--no-verify` (stage and model).
4. **Build:** `implementer` (`Build`) in its own worktree (naming Step 3's branch if created); open PR per `tracker-<tracker>.md`.
5. **Review:** `reviewer` (`Pull request`) with the PR; post review comment.
6. **Verify:** `tester` (`Pull request`, may run in parallel with Step 5; skip if no externally observable behavior); post test report.
7. **Fix loop:** if Review is `changes-needed` or Verify is `fail`:
   - Combined findings from parallel Review + Verify count as **1 round** (max 2 rounds; 3rd failure stops for owner).
   - **Code fault:** send findings to `implementer` on the same branch, then re-run Review and Verify on what changed. If `implementer` disputes a `must-fix` without changing code, post its rationale and re-check with `reviewer` (stop for owner if deadlocked).
   - **In-scope spec/design fault:** loop back to Step 1 or 2 **once** (counts as a round; re-run affected downstream steps including `test-author` if interfaces/checks changed). Scope changes, intent conflicts, or repeat failures stop for owner.
8. **Owner checks:** if checks include `(owner)` and `Process` is `light`, post evidence, add `needs-owner`, and wait for owner approval before merge. (In `full`, `(owner)` checks defer to the milestone demo.)
9. **Merge** (Review = `approve` and Verify = `pass` or skipped):
   1. Run `Check` yourself in a temporary detached worktree of the PR branch (unless `Check` is `none`), read the diff summary, and remove the worktree.
   2. File any accepted `proposed new issues` from subagents per `New issues placement` in `orchestration.md`, merge per `tracker-<tracker>.md` with the closing comment (what was built, key decisions, follow-up links, and in `light` proposals/cleanup ideas), and ensure the issue is closed.
   3. **Bootstrap check:** if this issue added or changed `Check` or `Run` (especially when `.agents/forge.md` has `Check: none` or `Run: README.md`), offer to update `.agents/forge.md` and `AGENTS.md` with owner approval and commit per `Approved documents` in `orchestration.md`.
