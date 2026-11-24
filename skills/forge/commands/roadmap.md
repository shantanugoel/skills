# forge roadmap <what changed>

You are the orchestrator. Change the direction of the project with the owner:

- Create or change the roadmap, the milestones, the spikes and the issues.
- Apply a spike answer or a milestone report to the documents.

The owner approves each change before you write it. Do not write code.

## Read first

1. `<forge>/reference/rules.md`.
2. `<forge>/reference/workflow.md`: "Process", "Tracking", "Spikes", "Brief for a subagent", "Delegation", "Documents
   that the owner approved" and "Utility tasks".
3. `.agents/forge.md`, and `<forge>/reference/tracker-<tracker>.md` for its "Tracker" setting.
4. `<forge>/reference/roster.md`. Apply the "Roster changes" of the settings, then the changes that the owner gave
   for this run.

## 1. Read the state

Read these items, if they exist:

- `docs/vision.md` and `docs/architecture.md`.
- The open spikes, and the spikes that closed after the last line in "Changes" (full process) or the last commit of
  `docs/vision.md` (light process).
- The open issues with the label `needs-owner`, and the Backlog issue.
- Full process: the Roadmap issue, the open milestones, and the report on the last milestone.

If `docs/vision.md` does not exist, recommend `forge kickoff`, and ask the owner.

## 2. Understand

If the owner gave no words, do a review. Find what is out of date, and propose a list of changes. Examples:

- A spike has an answer, and the documents do not use it.
- A milestone report has a "Learned" part that the roadmap does not use.
- An open question has an answer.
- A milestone is done.

If the owner gave words, tell back the change in one sentence and its kind:

| Kind | Example | What changes |
| --- | --- | --- |
| Create the first work | "kickoff stopped before init" | The spikes and the setup issue from the open questions |
| Create the roadmap | "make the roadmap, the spikes are done" | The Roadmap body. A milestone issue for each milestone. |
| Apply a spike answer | "spike 14 is answered" | "Choices" in the architecture, the open questions, the milestones that waited |
| Apply a milestone report | "M2 is accepted" | The later milestones and the documents, from the "Learned" part |
| Change a milestone | "add a milestone for sync", "do export before import" | The Roadmap body and the milestone issues |
| Add a spike | "we must know if X works before M3" | A spike issue and the open questions |
| Change the direction | "drop offline support", "also for teams" | The goals and the non-goals, the architecture, the milestones |

If the words can have two meanings, ask one question and wait. For a change of the direction, ask about the topics
that change, as step 4 of `<forge>/commands/kickoff.md` tells.

Light process: there is no Roadmap issue. A change is a change to the documents, and issues to create or close. If
the owner wants milestones with a demo, propose the full process. Then change the "Process" setting, and create the
Roadmap and Backlog issues as `forge init` tells.

## 3. Find out

Brief a researcher for a short question from outside, and an explorer for a question about the code. A question that
needs an experiment becomes a spike.

## 4. Draft

Draft the text. Do not write a file or a tracker change before step 7.

- For a small change, write the text yourself. Examples: one line, a new order, an answered question.
- If the vision changes, brief the planner (role `planner`, "For the vision").
- If the architecture changes, brief the designer (role `designer`, "For the architecture", step "Document").
- For new work or a new roadmap, brief the planner (role `planner`, "For the roadmap").

## 5. Challenge

For "Create the roadmap" and "Change the direction", brief the reviewer (role `reviewer`, "For a kickoff or a
roadmap"). Apply the findings that you agree with. Skip this step for a smaller change.

## 6. Show the owner

Show a table: what changes, where, and why. Add these items:

- The text of each new milestone, spike and issue.
- The findings of the reviewer that you did not apply.
- Your recommendation.

Apply the changes of the owner. Continue when the owner approves.

## 7. Apply

1. **Tracker.** Do these actions as the tracker file tells:
   - Create each new spike with the label `spike`, and each new issue with the label `enhancement`. Put them under
     Backlog if it exists.
   - Close each milestone, spike or issue that the change removes. Comment the reason first.
   - Full process: write the new Roadmap body, and add one line to "Changes".
   - Full process: create each new milestone issue with the label `milestone` and the Roadmap issue as its parent.
     The body has the goal, the demo, and "Plan: run `forge plan`".
   - Full process: if the change touches the milestone in progress, comment the change on its issue. Tell the owner
     which slices must change. Do not edit the slices here.
2. **Documents.** Link each new spike in the open questions of `docs/vision.md`. If a document or the settings
   changed, commit them as "Documents that the owner approved" in `workflow.md` tells.

## 8. Tell the owner

What changed, with links. The next command: `forge run <spike>`, `forge run <issue>`, `forge plan <milestone>`, or
none.
