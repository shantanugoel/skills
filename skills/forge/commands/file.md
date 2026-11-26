# forge file <what you saw or want>

Turn a rough bug report or feature request into an actionable issue. Do not fix it. Also read `<forge>/templates/issue.md`.

## Steps

1. **Understand:** restate the owner's intent in one sentence. If ambiguous, ask one clarifying question and wait; never ask what you can check yourself.
2. **Search duplicates:** search open and closed issues for the same subject. If an existing issue matches, show it and the new facts you would add, then ask whether to comment there:
   - Owner agrees → comment on it, return its ref, and stop.
   - Different problem → continue to Step 3.
   - Owner declines → stop.
3. **Reproduce (bugs only):** unless the owner asked to skip verification (record `not checked`), spend up to a few minutes reproducing on the default branch. Record exact steps and command output/screenshot (or `not seen`). Do not guess a root cause.
4. **Draft:** use `.github/ISSUE_TEMPLATE/` if present; otherwise use `Bug` or `Change` in `<forge>/templates/issue.md`. Preserve clear owner wording, include Step 3 evidence, and write draft acceptance checks—no design or fix.
5. **Create and place:** choose parent per `New issues` in `rules.md` (active milestone slice if breaking its checks/demo; else Backlog if present; else standalone). Label `bug` or `enhancement`. Use a behavior-focused title ("Export skips the last row", not "Fix export bug").
6. **Report to the owner:** return the issue ref, placement, and sizing verdict with reason:
   - Fits one PR → `forge run <issue>` can work on it now.
   - Larger than one PR → recommend splitting (`light`) or a milestone plan (`full`).
