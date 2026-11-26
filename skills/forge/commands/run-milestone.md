# forge run-milestone <milestone>

Execute every slice of an approved milestone without interrupting the owner except on stop conditions, then run the demo and stop for owner acceptance.

**Guards:**
- `Process` must be `full`; otherwise inform the owner and stop.
- `<milestone>` must already have slice issues (created after `forge plan` approval); otherwise tell the owner to run `forge plan <milestone>` and stop.

Also read `<forge>/commands/run.md`. Update `<milestone>` body to `State: in progress`.

## 1. Slice loop

1. List open slices of `<milestone>`. Pick the first in plan order whose `Needs` are all closed and that lacks `needs-owner`.
2. Execute `<forge>/commands/run.md` for that slice.
3. After each merge or closed spike, re-check remaining open slices. If the completed work changes a later slice's requirements, edit that slice and comment the reason on `<milestone>`. If the change expands milestone scope, trigger a stop condition.
4. Repeat. If a slice blocks on `needs-owner`, continue with independent slices. When no slice can proceed, report what is waiting and stop.

## 2. Finish milestone (when all slices are closed)

1. **Demo run:** brief `tester` (`Milestone demo`) to run the demo script on a clean default-branch worktree, saving evidence to `<main checkout>/<Evidence>/demo-<milestone>/`. Post the report on `<milestone>`. Any failure becomes a new slice under `<milestone>`—return to Step 1.
2. **Document check:** brief an `explorer` to compare all `Docs` (plus the `UI` doc and `AGENTS.md` if present) against the codebase for inaccuracies, omissions, or unclear steps. If findings exist, create one fix slice under `<milestone>` and run `forge run` for it.
3. **Report:** post on `<milestone>`:

   ```markdown
   ## Report
   **Built:** what a person can do now.
   **Demo:** result per demo step with evidence links, plus `(owner)` checks for the owner.
   **Left out:** planned items deferred, with issue links.
   **Learned:** proposed changes to later milestones or process (propose only; do not apply).
   **Cost:** slice count, review rounds, and owner stops.
   ```

4. **Owner acceptance:** add `needs-owner` to `<milestone>` and present the report and visual evidence. Once the owner completes `(owner)` checks and accepts, remove `needs-owner`, set `State: done`, close `<milestone>`, and tell the owner to apply `Learned` with `forge roadmap`.
