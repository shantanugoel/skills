# forge plan <milestone>

You are the orchestrator. Make one milestone into a plan that the owner can approve. Do not create slice issues, and
do not start a slice before the owner approves.

## Read first

1. `.agents/forge.md`. If the "Process" setting is not `full`, tell the owner that this command is for the full
   process. Ask if they want to change the process or use `forge run`. Then stop.
2. `<forge>/reference/workflow.md`, `<forge>/reference/rules.md`, and `<forge>/reference/tracker-<tracker>.md` for
   the "Tracker" setting.
3. `<forge>/reference/roster.md`. Apply the "Roster changes" of the settings, then the changes that the owner gave
   for this run.

## Steps

Brief each subagent in the form of "Brief for a subagent" in `workflow.md`.

1. **Read.** The milestone issue, the Roadmap issue, the Backlog issue, the documents of the project, and the report
   on the last milestone.
2. **Find the unknowns.** List what you must know before you can cut slices. Send an explorer or a researcher for
   each unknown that a short task can answer. An unknown that needs real work becomes the first slice, as a spike.
3. **Plan.** Brief the planner (role `planner`, "For a milestone"). It writes the plan as a draft comment on the
   milestone issue.
4. **Design.** If slices share a module boundary, a data shape or the API, brief the designer (role `designer`) for
   that part only. It adds one comment.
5. **Challenge.** Brief the reviewer (role `reviewer`, "For a milestone plan") with the draft and the design. Ask
   four questions:
   - What does the demo need that no slice builds?
   - Which slice does the demo not need?
   - Is the largest unknown early enough?
   - Which flag is missing or not necessary?
6. **Settle.** Apply the answers that you agree with. Then put the plan in the body of the milestone issue.
7. **Stop for the owner.** Add the label `needs-owner`. Tell the owner, in a few lines: the goal, the demo, the slices
   as a table (title, flags), the new dependencies, the `(owner)` checks, and each open question in the form of
   "Writing for a person" in `rules.md`.

## After the owner approves

1. Apply the changes that the owner asked for.
2. Create one issue for each slice, in the order of the plan, with the milestone as its parent. The body has the
   goal, the draft checks, the flags and the needs, in the form of the planner role. In each "Needs" line, replace
   the slice numbers of the plan with the references of the issues that you created. A spike slice uses the spike
   form of `<forge>/templates/issue.md` and the label `spike`.
3. Remove `needs-owner`. Tell the owner that `forge run-milestone <milestone>` can start.
