# forge kickoff <idea>

Act as orchestrator and thinking partner to turn an idea into `docs/vision.md`, `docs/architecture/`, `docs/design-language.md` (if UI), and the first spikes/setup issue. Do not write code. Perform **no tracker actions** before Step 8 (after owner approval in Step 7).

Also read `<forge>/templates/vision.md`, `<forge>/templates/architecture.md`, `<forge>/templates/design-language.md`, and `Spike` in `<forge>/templates/issue.md`.

## 1. Assess current state

- Check git repo, commits, and `.agents/forge.md` (if `docs/vision.md` exists and `Roadmap` is set, recommend `forge roadmap`).
- If `docs/vision.md` exists, summarize goals and open questions; ask to continue from open questions (recommended) or restart.
- If code exists, brief an `explorer` to summarize it; treat code as fact, not proposal.

## 2. Capture

Restate the idea in 2–3 sentences, list knowns and largest unknowns, and ask for missing links/files plus any specific research question.

## 3. Research

Run `researcher` tasks in parallel for each focus not already answered by owner materials (≤1-screen summary each):

| Focus | Question |
| --- | --- |
| Prior art | Existing products/OSS, strengths, and user complaints. |
| Stack | Fitting languages, frameworks, libraries, and services (maturity, license, cost). |
| Pitfalls | Known domain traps and how similar projects fail. |
| Owner's question | If provided in Step 2. |

Present a combined summary table, highlighting surprises and idea-changing findings.

## 4. Interview

Ask **one question at a time**, recommended option first (2–4 options when helpful, answerable in one word). Skip what research already answered; challenge contradictions and scope creep. Use `orchestration.md`'s Owner Question form only for costly trade-offs; summarize decisions every ~5 questions.

Cover in order (skip clear topics):
1. **Problem:** who has it, one concrete example, current workaround.
2. **Prior art:** why existing options fall short.
3. **Success:** end-to-end scenario of the first useful version.
4. **Non-goals:** what we explicitly will not build.
5. **UI / screens:** whether the project has screens; if yes, target users/devices and rough visual/interaction feel.
6. **Constraints:** platform, language, cost, paid models, privacy.
7. **Appetite:** time worth investing; solo tool or multi-user product.
8. **Process:** recommend `light` vs `full` per `orchestration.md` (skip if `.agents/forge.md` exists).

Unanswered items go to `Open questions`. If the owner stops before Step 7, save an uncommitted draft `docs/vision.md` with open topics so the next kickoff resumes there.

## 5. Shape and draft

1. **Options:** Brief `designer` (`Architecture options`) and—if UI—`ux-designer` (`Design language options`) in parallel. Owner picks or blends; resolve remaining stack/UI choices one question at a time.
2. **Documents:** Brief `planner` (`Vision`), `designer` (`Architecture docs`), and—if UI—`ux-designer` (`Design language doc`) in parallel.
3. **First work:** Brief `planner` (`Roadmap`) with drafted docs and combined unknowns: 2–4 decision-blocking spikes and 1 setup+check issue (milestones and the Roadmap body wait for `forge roadmap` after spikes close).

## 6. Challenge

Brief `reviewer` (`Kickoff or roadmap`) with drafted docs and first work; apply agreed findings.

## 7. Settle with the owner

Present in ~1 screen: vision summary (goals/non-goals), chosen architecture and UI direction (if any), first-work table (`title`, `kind`, `question/goal`), unapplied reviewer findings with rationale, and process. Apply owner edits; once approved, write `docs/vision.md`, `docs/architecture/`, and (if UI) `docs/design-language.md` without committing yet.

## 8. Set up repository and settings

Ask before each step; skip completed steps:
1. **Git:** if not a git repo, offer `git init`.
2. **Init & remote:** if `.agents/forge.md` is absent:
   - Ask `github` vs `local` tracker.
   - If `github`, git repo exists, and no GitHub remote exists, offer `gh repo create <owner>/<name> --private --source=. --remote=origin`.
   - Offer `<forge>/commands/init.md` now (passing process, tracker, kickoff docs, `UI` setting, and noting setup+check issue is already planned).
3. **Existing settings:** if `.agents/forge.md` exists, offer to add kickoff docs to `Docs` and set `UI` if applicable.

If the owner declines `forge init`: commit written docs per `Approved documents` in `orchestration.md` **if** a git repo exists, then stop and tell the owner to run `forge init` and `forge roadmap`.

## 9. Create first work and commit

1. Read `<forge>/reference/tracker-<tracker>.md` if not yet loaded.
2. Create spikes (`spike`) and setup issue (`enhancement`) under Backlog if it exists.
3. Link each spike in `docs/vision.md` under `## Open questions`.
4. Commit approved docs, init files (`.agents/forge.md`, `.gitignore`, project instructions), and `.agents/issues/` (if `local`) per `Approved documents` in `orchestration.md`.

## 10. Report to the owner

List written docs and created issues with links, plus next steps: `forge run <spike>` → `forge run` for the setup issue → `forge roadmap` (→ `forge plan` in `full`).
