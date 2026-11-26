# forge plan <milestone>

Turn one milestone into an owner-approved plan and slice list. Do not create slice issues or start building until approved.

**Guard:** if `Process` is not `full`, tell the owner this requires `full` (ask whether to switch or use `forge run`) and stop.

## 1. Draft the plan

1. **Read:** milestone issue, Roadmap, Backlog, project docs (including `UI` doc if set), and last milestone report.
2. **Resolve unknowns:** `explorer`/`researcher` for quick questions; larger unknowns become an early spike slice.
3. **Plan:** `planner` (`Milestone`); post draft comment on milestone issue.
4. **Cross-slice design (only for shared contracts, per `orchestration.md` order):** `ux-designer` (`Milestone UI`) for shared shell/navigation/primitives (`UI` ≠ `none`); `designer` (`Issue or milestone design`) for shared modules/data/APIs. Post comment(s).
5. **Challenge:** `reviewer` (`Milestone plan`) with draft plan and design comments; post comment.
6. **Settle:** apply agreed findings, then write settled plan into milestone issue body.
7. **Stop for owner:** add `needs-owner` and summarize: goal, demo, slices table (`title`, `flags`), backlog triage, new dependencies, `(owner)` checks, and open questions (`orchestration.md` Owner Question form).

## 2. After owner approval

1. Apply owner edits to milestone issue body and set `State: next`.
2. Execute approved `Backlog triage` decisions (move into milestone, keep, or close with reason).
3. Create slice issues in plan order with `<milestone>` as parent (`Issue` or `Spike` in `<forge>/templates/issue.md`; resolve plan slice numbers in `Needs` to created issue refs; label spikes `spike`).
4. Remove `needs-owner`, commit updated `.agents/issues/` if `local` tracker (per `Approved documents`), and tell owner `forge run-milestone <milestone>` is ready.
