# forge run <issue>

You are the orchestrator. Take one issue from its text to a merged pull request. The issue is a slice of a
milestone, or a bug or a small change outside a milestone.

## Read first

1. `<forge>/reference/workflow.md`: the stages, the flags, the stop conditions, the brief and the delegation.
2. `<forge>/reference/rules.md`.
3. `.agents/forge.md`, and `<forge>/reference/tracker-<tracker>.md` for its "Tracker" setting.
4. `<forge>/reference/roster.md`. Apply the "Roster changes" of the settings, then the changes that the owner gave
   for this run.

## Before you start

- A slice has a parent milestone with an approved plan. An issue outside a milestone needs no plan, but it must be
  small: one pull request. If it is larger, tell the owner that it needs a split (light process) or a milestone
  (full process), and stop.
- Each issue under "Needs" is closed.
- The default branch passes the check, if the check exists. An issue that adds the check is permitted.

If one of these is not true, tell the owner and stop.

## Spikes

If the issue has the label `spike`, do the stages of "Spikes" in `workflow.md`, not the steps below. Brief the
planner, the implementer and the reviewer in the form of "Brief for a subagent" in `workflow.md`. Tell each one that
the issue is a spike.

## Steps

Brief each subagent in the form of "Brief for a subagent" in `workflow.md`.

1. **Spec.** Brief the planner (role `planner`, "For an issue"). Read the result: a tester must be able to see each
   check. A slice must stay inside the milestone plan. For a bug, the planner uses the bug form. For a small issue,
   you can write the spec yourself in the same form.
2. **Design**, for the flag `design`. Brief the designer (role `designer`).
3. **Tests first**, for the flag `test-first`. Brief the test author (role `test-author`) in its own worktree. It
   sends back the branch with failing acceptance tests.
4. **Build.** Brief the implementer (role `implementer`) in its own worktree. If step 3 made a branch, name it in the
   brief. The implementer sends back the pull request.
5. **Review.** Brief the reviewer (role `reviewer`) with the pull request.
6. **Verify.** Brief the tester (role `tester`) with the pull request. You can start it at the same time as the
   review. Skip it when the change has no behavior that a person or a caller can see.
7. **Fix.** If the review or the test failed, send the findings to the implementer, with the branch and the pull
   request. Then do steps 5 and 6 again for what changed. Do a maximum of two rounds. A finding about the spec or the
   design goes back to step 1 or 2, and counts as a round.
8. **Merge.** When the verdict is `approve`, and the result is `pass` or you skipped step 6:
   1. Run the check on the branch yourself, in a temporary worktree (refer to "Checkouts" in `workflow.md`).
   2. Merge the pull request.
   3. Comment on the issue: what was built, each decision, each follow-up as a link to a new issue, and (light
      process) each proposal or cleanup idea. Close the issue if the merge did not close it.

## Record

After each stage, comment on the issue: the stage, the model, the result. On a stop condition, comment the question
and your recommendation, add the label `needs-owner`, and stop this issue.
