# forge plan <milestone>

Turn one milestone into an owner-approved plan and slice list. Do not create slice issues or start building until the owner approves.

**Guard:** if `Process` is not `full`, tell the owner this command requires `full` process (ask whether to switch or use `forge run`) and stop.

## 1. Draft the plan

1. **Read:** the milestone issue, Roadmap, Backlog, project docs (including `UI` doc if set), and last milestone report.
2. **Resolve unknowns:** use `explorer`/`researcher` for quick questions; larger unknowns become an early spike slice.
3. **Plan:** brief `planner` (`Milestone`) and post its draft as a comment on the milestone issue.
4. **Cross-slice design (only if slices share contracts):**
   - Shared UI shell, navigation, or primitives (when `UI` ≠ `none`) → `ux-designer` (`Milestone UI`), post comment.
   - Shared module boundaries, data shapes, or APIs → `designer` (`Issue or milestone design`), post comment.
   - When both apply, run `ux-designer` → `designer` (or in parallel if APIs are fixed).
5. **Challenge:** brief `reviewer` (`Milestone plan`) with the draft plan and design comments; post its review comment.
6. **Settle:** apply findings you agree with, then write the settled plan into the milestone issue body.
7. **Stop for owner:** add `needs-owner` and present concisely: goal, demo, slices table (`title`, `flags`), backlog triage decisions, new dependencies, `(owner)` checks, and open questions (using `rules.md` Owner Question form).

## 2. After owner approval

1. Apply owner edits to the milestone issue body and set `State: next`.
2. Execute approved `Backlog triage` decisions (move items into this milestone, keep, or close with reason).
3. Create slice issues in plan order with `<milestone>` as parent (use `Issue` or `Spike` form from `<forge>/templates/issue.md`; replace plan slice numbers in `Needs` with created issue refs; label spikes `spike`).
4. Remove `needs-owner`. For `local` tracker, commit updated `.agents/issues/` per `Approved documents` in `orchestration.md`.
5. Tell the owner `forge run-milestone <milestone>` is ready to start.
