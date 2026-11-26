# Issue templates

Single source of truth for issue forms across `forge file`, `forge plan`, `forge kickoff`, `forge roadmap`, and `planner`. Remove empty optional sections, but always keep `## Goal` and `## Acceptance checks` (or all sections for `Spike`).

## Issue (slice or standalone spec)

```markdown
## Goal
What a person or caller can do after this change.

## Acceptance checks
- [ ] <observable pass/fail behavior from outside>

## Out of scope

## Notes
Needs: <issue refs or none>. Flags: <ui, design, test-first, invariant, or none>.
```

## Bug

Used by `forge file` (when the repo has no `.github/ISSUE_TEMPLATE/`) and refined by `planner` in `forge run`. **Preserve `## Checked` when refining.**

```markdown
## What occurs
Numbered reproduction steps, then actual output (command + output, or screenshot). One real example.

## What must occur
Expected result for the same steps.

## Checked
On default branch at <commit>: seen | not seen | not checked (owner requested filing without check).

## Goal
What a person or caller can do after the fix.

## Acceptance checks
- [ ] The steps in "What occurs" produce the result in "What must occur".
- [ ] A test fails without the fix and passes with it.

## Out of scope

## Notes
Owner's words if helpful. Needs: <issue refs or none>. Flags: <flags or none>.
```

## Change

Used by `forge file` for feature/change requests and refined by `planner` in `forge run`. **Preserve `## Why` when refining.**

```markdown
## Why
The need in the owner's words, with one concrete example of a user or caller.

## Goal
What a person or caller can do after this change.

## Acceptance checks
- [ ] <observable pass/fail behavior from outside>

## Out of scope

## Notes
Owner's words if helpful. Needs: <issue refs or none>. Flags: <flags or none>.
```

For `forge file` (Bug and Change): write draft acceptance checks only—do not add a design or fix.

## Spike

```markdown
## Question
One specific question with a concrete example ("Can X do Y under Z?", not "Look into X").

## Why it is important
The decision blocked by this answer, and which docs or milestones depend on it.

## Options
Candidate answers to compare. Always include "None of these".

## Evidence
What proves the answer (measurement, working call, documented limit — quantify where possible).

## Time box
Maximum effort (e.g., "one implementer run"). When reached, return partial findings.

## Out of scope
```

## Spike answer

Returned by `implementer` or `researcher` and posted on the spike issue by the orchestrator before review.

```markdown
**Answer:** one sentence (or "not answered" and why).
**Evidence:** commands + output, measurements, links. State what was run vs only read.
**Recommendation:** chosen option and one-sentence reason.
**Still unknown:** what the experiment did not cover.
```
