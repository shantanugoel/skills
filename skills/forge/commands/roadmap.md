# forge roadmap <what changed>

Update project direction, roadmap, milestones, spikes, issues, and design/vision docs with owner approval. Do not write code.

## 1. Read current state

Read what exists:
- `docs/vision.md`, `docs/architecture.md`, and the `UI` doc (if set).
- Open spikes, plus spikes closed since the last `## Changes` entry (`full`) or last `docs/vision.md` commit (`light`).
- Open `needs-owner` issues and Backlog.
- `full` process: Roadmap issue, open milestones, and last milestone report.

If `docs/vision.md` is missing, recommend `forge kickoff` and ask the owner how to proceed.

## 2. Understand the change

- **No arguments:** audit for drift—unapplied spike answers, milestone `Learned` items, answered open questions, completed milestones, and stale `Check: none` / `Run` / `AGENTS.md` once setup code exists—and propose updates.
- **With arguments:** restate the change in one sentence. Ask one clarifying question if ambiguous. For major direction shifts, interview on affected Step 4 topics from `<forge>/commands/kickoff.md`.
- **`light` process:** updates target docs and issues directly. If the owner wants milestones and demos, propose switching `Process` to `full`, updating `.agents/forge.md`, and creating Roadmap/Backlog issues.

## 3. Investigate

Use `researcher` for quick external facts and `explorer` for codebase questions. Anything needing an experiment becomes a `spike`.

## 4. Draft (no file or tracker writes yet)

- Small edits (reordering, one-line updates, answered questions): draft yourself.
- Vision changes → `planner` (`Vision`).
- Architecture changes → `designer` (`Architecture doc`).
- Visual/UX direction changes (when `UI` ≠ `none`) → `ux-designer` (`Design language doc`).
- New roadmap, milestones, spikes, or issues → `planner` (`Roadmap`).

## 5. Challenge

For creating the firm initial roadmap or changing product direction, brief `reviewer` (`Kickoff or roadmap`) and apply agreed findings. Skip for smaller updates.

## 6. Confirm with the owner

Show a table of **what changes, where, and why**, plus full text of new milestones/spikes/issues, unapplied reviewer findings, and your recommendation. Wait for approval and apply edits.

## 7. Apply

1. **Tracker:**
   - Create new spikes (`spike`) and issues (`enhancement`) under Backlog if it exists.
   - Close removed milestones, spikes, or issues (comment reason first).
   - `full` process: update Roadmap body (append to `## Changes`), create new milestone issues (`milestone` label, parent = Roadmap, body with `State: candidate` or `next`, `## Goal`, `## Demo`, `## Waits on`, optional `## Out of scope` for boundaries agreed here—no slices or *how*—and `"Plan: run forge plan"`). If the active milestone is affected, comment on it and list slices needing updates—do not edit slices here.
2. **Docs and commit:**
   - Link new spikes in `docs/vision.md` under `## Open questions`.
   - If any docs, `.agents/forge.md`, or local `.agents/issues/` files changed, commit them per `Approved documents` in `orchestration.md`.

## 8. Report to the owner

Summarize changes with links and the next command (`forge run <spike>`, `forge run <issue>`, `forge plan <milestone>`, or none).
