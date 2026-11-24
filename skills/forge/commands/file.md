# forge file <what you saw or what you want>

The owner tells you about a bug or a wish in a few rough words. Make it into an issue that another agent can work
on with no questions. Do not fix it.

Read first:

- `<forge>/reference/rules.md`. "Writing for a person" is the rule for the text.
- `.agents/forge.md`, and `<forge>/reference/tracker-<tracker>.md` for its "Tracker" setting.
- `<forge>/roles/planner.md`. It has the forms of an issue.

## Steps

1. **Understand.** Tell back in one sentence what the owner means. If the words can have two meanings, ask one
   question and wait. Do not ask about what you can find out yourself.
2. **Look.** Find issues with the same subject, open and closed. If an issue covers it, comment the new facts on that
   issue, tell the owner, and stop.
3. **Check, for a bug.** Try the steps on the default branch. Use a few minutes, not more. Write down what you saw:
   the command and its output, or a screenshot. If you cannot see the bug, tell this in the issue. Do not guess a
   cause.
4. **Write.** If the project has issue templates in `.github/ISSUE_TEMPLATE/`, use the applicable one. If not, use
   the bug form or the issue form of the planner role. Keep the words of the owner where they are clear. Add what you
   saw in step 3. Do not add a design or a fix.
5. **Place.**

   | The issue | Where it goes |
   | --- | --- |
   | It breaks an acceptance check or the demo of the milestone that is in progress (full process: list the open issues with the label `milestone`) | Under that milestone, as a slice |
   | All other issues, if the project has a Backlog issue | Under Backlog |
   | All other issues, if the project has no Backlog issue | No parent |

   Create the issue with the label `bug` or `enhancement`. The title tells the behavior in plain words: "The export
   skips the last row", not "Fix export bug".
6. **Tell the owner.** Give the reference, where you put it, and one of these, with the reason:
   - "`forge run <issue>` can fix it now".
   - Light process: "this is larger than one pull request. Split it into smaller issues."
   - Full process: "this is larger than one pull request. It needs a milestone plan."
