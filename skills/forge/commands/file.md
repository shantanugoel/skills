# forge file <what you saw or want>

Turn a rough bug report or feature request into an actionable issue. Do not fix it. Also read `<forge>/templates/issue.md`.

## Steps

1. **Understand:** restate intent in one sentence. Ask one clarifying question if ambiguous; never ask what you can check yourself.
2. **Search duplicates:** search open and closed issues. If one matches, show it plus new facts and ask whether to comment there:
   - Agrees → comment, return ref, stop.
   - Different problem → Step 3.
   - Declines → stop.
3. **Reproduce (bugs only):** unless the owner asked to skip verification (`not checked`), spend a few minutes reproducing on the default branch. Record steps and actual output/screenshot (or `not seen`). Never guess a root cause.
4. **Draft:** use `.github/ISSUE_TEMPLATE/` if present, else `Bug` or `Change` in `<forge>/templates/issue.md`. Keep clear owner wording, include Step 3 evidence, and write draft checks—no design or fix.
5. **Create and place:** place per `New issues placement` in `orchestration.md`, label `bug` or `enhancement`, and use a behavior-focused title ("Export skips the last row", not "Fix export bug").
6. **Report:** return issue ref, placement, and sizing verdict: fits one PR (`forge run <issue>`), or larger (recommend splitting in `light` or a milestone plan in `full`).
