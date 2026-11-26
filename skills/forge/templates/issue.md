# Issue templates

Single source of truth for issue forms across `forge file`, `forge plan`, `forge kickoff`, `forge roadmap`, and `planner`. Remove empty optional sections, keeping `## Goal` and `## Acceptance checks` (or all sections for `Spike`).

## Issue (base form for slices and standalone specs)

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

Prepend these sections to `## Issue` (used by `forge file` when `.github/ISSUE_TEMPLATE/` is absent, and refined by `planner`—**always preserve `## Checked`**):

```markdown
## What occurs
Numbered reproduction steps, then actual output (command + output, or screenshot). One real example.

## What must occur
Expected result for the same steps.

## Checked
On default branch at <commit>: seen | not seen | not checked (owner requested filing without check).
```

Required bug acceptance checks:
- [ ] The steps in "What occurs" produce the result in "What must occur".
- [ ] A test fails without the fix and passes with it.

## Change

Prepend this section to `## Issue` (refined by `planner`—**always preserve `## Why`**):

```markdown
## Why
The need in the owner's words, with one concrete example of a user or caller.
```

*(For `forge file` on Bug/Change: write draft acceptance checks only; never add a design or fix.)*

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

Returned by `implementer` or `researcher`; posted on the spike issue by the orchestrator before review.

```markdown
**Answer:** one sentence (or "not answered" and why).
**Evidence:** commands + output, measurements, links. State what was run vs only read.
**Recommendation:** chosen option and one-sentence reason.
**Still unknown:** what the experiment did not cover.
```
