# forge plan <milestone>

Turn one milestone into an owner-approved plan and slice list. Do not create slice issues or start building until approved.

**Guard:** if `Process` is not `full`, tell the owner this requires `full` (ask whether to switch or use `forge run`) and stop.

## 1. Draft the plan

1. **Read:** milestone issue, Roadmap, Backlog, project docs (including `UI` doc if set), and last milestone report.
2. **Resolve unknowns:** `explorer`/`researcher` for quick questions; larger unknowns become an early spike slice.
3. **Plan:** `planner` (`Milestone`) drafts the plan and surfaces unresolved decisions, edge cases, and assumptions (do not post the unsettled draft as a comment).
4. **Grill / clarify (before design):** Resolve every open question or risky assumption from Step 3 (plus any gaps you spot) with the owner—**one question at a time**, recommended option first (2–4 options when helpful; use `orchestration.md`'s Owner Question form for costly trade-offs). Skip anything code/docs already answer (skip this step if nothing is ambiguous). Apply answers to the draft, re-briefing `planner` if scope or slices change materially, and post one concise comment summarizing key owner decisions if any were made.
5. **Cross-slice design (only for shared contracts, per `orchestration.md` order):** `ux-designer` (`Milestone UI`) for shared shell/navigation/primitives (`UI` ≠ `none`); `designer` (`Issue or milestone design`) for shared modules/data/APIs. Fold settled `## UX/UI design` / `## Design` sections into the milestone draft (clarify any new owner decisions before Step 6).
6. **Challenge:** `reviewer` (`Milestone plan`) with the settled draft (including any cross-slice design); post review comment.
7. **Settle:** apply agreed findings, then write the settled plan (including any cross-slice `## UX/UI design` / `## Design` sections) into the milestone issue body.
8. **Stop for owner approval:** add `needs-owner` and summarize: goal, demo, slices table (`title`, `flags`), backlog triage, new dependencies, `(owner)` checks, and any remaining open questions (`orchestration.md` Owner Question form).

## 2. After owner approval

1. Apply owner edits to milestone issue body and set `State: next`.
2. Execute approved `Backlog triage` decisions (move into milestone, keep, or close with reason).
3. Create slice issues in plan order with `<milestone>` as parent (`Issue` or `Spike` in `<forge>/templates/issue.md`; resolve plan slice numbers in `Needs` to created issue refs; label spikes `spike`).
4. Remove `needs-owner`, commit updated `.agents/issues/` if `local` tracker (per `Approved documents`), and tell owner `forge run-milestone <milestone>` is ready.
