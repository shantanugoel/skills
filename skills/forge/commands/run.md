# forge run <issue>

Take one issue (or spike) from spec to merged change (or closed answer). All tracker writes and brief stage comments (`stage, model, result`) are performed by the orchestrator.

## 1. Read issue and check for spike

Read `<issue>` first.

**If labeled `spike`**, execute only these stages and stop:
1. **Spec:** brief `planner` (`Spike`)—or refine yourself if already crisp—and update the issue body.
2. **Experiment:** brief `implementer` (`Spike`) in a worktree (or `researcher` without a worktree if no code is needed). Post the returned `Spike answer` as a comment on the issue. *(Exhausting the time box with partial findings is a valid result, not a failure.)*
3. **Review:** brief `reviewer` (`Spike`). Post the review comment. On `changes-needed`, send findings back to `implementer`/`researcher` (max 2 fix rounds; 3rd failure stops for owner).
4. **Close:** delete the experiment branch (local + remote if pushed) and close the issue. For standalone spikes, tell the owner to apply the answer with `forge roadmap` (`run-milestone` handles milestone spikes).

## 2. Preconditions (regular issues)

Verify before starting (if any fails, inform the owner and stop):
- If a slice, its parent milestone has an approved plan. If standalone, it fits one PR (else advise splitting in `light` or a milestone in `full`).
- Every issue listed under `Needs` is closed.
- Default branch passes `Check` (skip if `Check` is `none` or this issue adds `Check`).

## 3. Stages

1. **Spec:** brief `planner` (`Issue`), or write the spec yourself for a small issue (`templates/issue.md`). Verify all checks are observable and within milestone scope, then update the issue body.
2. **Design (by flag):**
   - If `ui` flag (and `UI` ≠ `none`): brief `ux-designer` (`Screen design`) and post its comment.
   - If `design` flag: brief `designer` (`Issue or milestone design`) and post its comment.
   - When both `ui` and `design` apply, run `ux-designer` → `designer` by default (or in parallel if the API/data contract is already fixed).
3. **Tests first (`test-first` flag):** brief `test-author` in its own worktree. Post the stage comment noting `--no-verify` was used for intentionally failing tests.
4. **Build:** brief `implementer` (`Build`) in its own worktree (naming the branch if Step 3 created one). Open the PR using the returned PR title/body per `tracker-<tracker>.md`.
5. **Review:** brief `reviewer` (`Pull request`) with the PR. Post the review comment.
6. **Verify:** brief `tester` (`Pull request`) with the PR (may run in parallel with Step 5; skip if the change has no externally observable behavior). Post the test report.
7. **Fix loop:** if Review is `changes-needed` or Verify is `fail`:
   - Combined findings from a parallel Review + Verify pass count as **1 round** (max 2 rounds; a 3rd failure triggers a stop condition).
   - **Code fault:** send findings to `implementer` on the same branch, then re-run Review and Verify for what changed. If `implementer` disputes a `must-fix` without changing code, post its rationale and re-check with `reviewer` (stop for owner if deadlocked).
   - **In-scope spec or design fault:** loop back to Step 1 or Step 2 **once** (counts as a round; re-run affected downstream steps, including `test-author` if interfaces/checks changed). If fixing it changes scope, contradicts owner intent, or fails again, trigger a stop condition.
8. **Owner checks:** if acceptance checks include `(owner)` and `Process` is `light`, post evidence, add `needs-owner`, and stop until the owner confirms before merging. (In `full` process, `(owner)` checks defer to the milestone demo.)
9. **Merge** (when Review is `approve` and Verify is `pass` or skipped):
   1. Check out the PR branch in a temporary detached worktree, run `Check` yourself (unless `Check` is `none`), inspect the diff summary, and remove the temporary worktree.
   2. Draft the closing comment: what was built, key decisions, follow-up issue links, and (`light` process) notable proposals/cleanup ideas.
   3. Merge per `tracker-<tracker>.md` (for `local`, write the closing comment and `Status: closed` **before** committing the squash merge; for `github`, squash-merge, then post the closing comment and close the issue if still open).
