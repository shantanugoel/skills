# Issue templates

`forge file` uses these forms when the project has no issue templates. Use the bug form for a defect, and the change
form for a wish or a new need. Delete a section that has nothing in it, except "Goal" and "Acceptance checks".
`forge kickoff`, `forge roadmap` and `forge plan` use the spike form for a question that blocks a decision.

## Bug

```
## What occurs
The steps to see the bug, as a numbered list. Then what you see: the command and its output, or a screenshot.
One real example.

## What must occur
The correct result for the same steps.

## Checked
On the default branch at <commit>: seen | not seen | not checked (the owner asked to file it without a check).

## Goal
What a person or a caller can do after the fix.

## Acceptance checks
- [ ] The steps in "What occurs" give the result in "What must occur".
- [ ] A test fails without the fix and passes with it.

## Out of scope

## Notes
The words of the owner, if they help. Related issues.
```

## Change

```
## Why
The need, in the words of the owner. One real example of a person or a caller who has the need.

## Goal
What a person or a caller can do after this change.

## Acceptance checks
- [ ] <something that a tester can see pass or fail from outside>

## Out of scope

## Notes
The words of the owner, if they help. Related issues.
```

For the bug form and the change form:

- Write the acceptance checks as a draft. The planner makes them firm in `forge run`.
- Do not add a design or a fix.

## Spike

```
## Question
One question, with one real example. "Can X do Y under Z?", not "Look into X".

## Why it is important
The decision that waits for the answer, and the documents or milestones that change with it.

## Options
The answers that we decide between. "None of these" is always an option.

## Evidence
What answers the question: a measurement, a working call, a limit in the documents. Give a number where you can.

## Time box
The maximum work, for example "one implementer run". When it ends, send back what you found.

## Out of scope
```

## Spike answer

The implementer or the researcher writes this comment on the spike issue.

```
**Answer:** one sentence. Or "not answered", and the reason.
**Evidence:** the commands and their output, the numbers, the links. Tell what you ran and what you only read.
**Recommendation:** the option, and the reason in one sentence.
**Still unknown:** what the experiment did not show.
```
