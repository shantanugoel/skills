# Issue templates

`forge file` uses these forms when the project has no issue templates. Use the bug form for a defect, and the change
form for a wish or a new need. Delete a section that has nothing in it, except "Goal" and "Acceptance checks".

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

- Write the acceptance checks as a draft. The planner makes them firm in `forge run`.
- Do not add a design or a fix.
