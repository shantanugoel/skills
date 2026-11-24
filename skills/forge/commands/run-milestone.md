# forge run-milestone <milestone>

You are the orchestrator. Do each slice of an approved milestone, then stop for the demo. Work without the owner
between the plan and the demo, except on a stop condition.

## Read first

1. `.agents/forge.md`. If the "Process" setting is not `full`, tell the owner that this command is for the full
   process, and stop.
2. `<forge>/commands/run.md`. You do it for each slice.

## Before you start

The milestone has slice issues. They exist only after the owner approved the plan. If it has none, tell the owner to
run `forge plan <milestone>`, and stop.

## Loop

1. List the open slices of the milestone. Select the first slice, in the order of the plan, whose "Needs" are all
   closed and that does not have `needs-owner`.
2. Do `forge run` for it.
3. After the merge, read the open slices again. If the merged work changed what one of them needs, edit that slice
   and comment the reason on the milestone issue. If the change adds scope to the milestone, it is a stop condition.
4. Do these steps again. When a slice stops for the owner, continue with slices that do not need it. When no slice
   can continue, tell the owner what waits, and stop.

## When all slices are closed

1. **Demo run.** Brief the tester (role `tester`, "For a milestone demo") to do the demo script on the default branch
   from a clean start. It saves the evidence under `<evidence directory>/demo-<milestone>/`. A failure becomes a new
   slice. Go back to the loop.
2. **Document check.** Brief an explorer to compare the documents that the "Docs" setting names with the code: what
   is wrong, what is missing, what a new reader cannot follow. If there are findings, create one slice issue for them
   under the milestone, and do `forge run` for it.
3. **Report.** Comment on the milestone issue:

   ```
   ## Report
   **Built:** what a person can do now.
   **Demo:** the result of each demo step with its evidence, and the `(owner)` checks that the owner must do.
   **Left out:** what the plan had and the milestone does not have, with the issue for each.
   **Learned:** what must change in later milestones or in the way of work. Propose the change. Do not apply it.
   **Cost:** the slices, the review rounds, and each stop for the owner.
   ```

4. **Stop for the owner.** Add the label `needs-owner` to the milestone. Show the owner the report and the
   screenshots. The owner does the `(owner)` checks and accepts the milestone.
   After that, apply the changes to later milestones that the owner agreed to, and close the milestone.
