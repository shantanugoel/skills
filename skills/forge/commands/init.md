# forge init

Make the project ready for forge. Find each setting that you can find yourself. Ask the owner only about the rest.
Do not change code.

Read first: `<forge>/reference/workflow.md` ("Settings", "Tracker" and "Process"), `<forge>/reference/roster.md`, and
`<forge>/templates/forge.md`.

## 1. Explore

Read what exists. Do not guess.

- `.agents/forge.md`. If it exists, forge was set up before. Use its values as the proposals, and change only what the
  owner changes.
- `git remote -v`. Is the repository on GitHub? Run `gh repo view --json nameWithOwner,isFork,parent` to make sure
  that `gh` can reach it, and to find the repository that gets the issues. If the repository is a fork, ask the owner
  if the issues go to the fork or to the parent. For the parent, write the "Repository" setting.
- `README.md`, `AGENTS.md`, `CLAUDE.md`, the build files, the CI configuration, the `scripts/` directory, the git
  hooks, `.github/`, and the list of documents.
- Signs of a release: tags, a published package, a changelog.

## 2. Ask

Tell the owner in a few lines what you found. Then ask the questions in this order. Ask one question, wait for the
answer, then ask the next. Put the recommended answer first, so that the owner can accept it with one word. Skip a
question when the exploration answered it clearly, and tell the owner the value that you used.

1. **Process.** `light` or `full`. Explain the difference in two lines (refer to "Process" in `workflow.md`).
   Recommend `light`, unless the project is a product with a plan in steps.
2. **Tracker.** `github` if a remote is on GitHub and `gh` can reach it. If not, `local`. With `github`, the
   repository must be on GitHub. If it is not, ask for the URL, or use `local`.
3. **Check.** One command that checks format, lint and tests. Propose the command that CI runs, or a script that
   runs the commands that you found. If no check exists, propose to make one as the first issue.
4. **Run.** How a tester starts the real program. Propose the steps from `README.md` or the build files. For a
   library with no program, propose "call the public API from a test program".
5. **Docs.** The documents to keep correct. Propose the documents that you found, with one line about each.
6. **Invariants.** Rules that a change must not make weaker. Propose some from what you read, or "none".
7. **Users and devices.** Ask only if the project has screens.
8. **Released.** Ask only if the exploration did not show it.
9. **Models.** Ask only if the project calls a model.
10. **Roster.** Show the roles of the default roster in one short table. Ask if it is correct for this project.
    Recommend "yes".

Use the default of `workflow.md` for each other setting.

## 3. Confirm

Make the draft of `.agents/forge.md` from the template. Write each setting in the table, also the settings that have
the default value, so that the owner can see and edit all of them. Show the draft to the owner. Let the owner change
it.

## 4. Write

1. Write `.agents/forge.md`.
2. Add the evidence directory to `.gitignore`.
3. Add this block to the project instructions, so that each agent knows about forge. If `CLAUDE.md` exists and does
   not only import `AGENTS.md`, edit `CLAUDE.md`. Else, if `AGENTS.md` exists, edit `AGENTS.md`. If neither exists,
   ask the owner which file to create. If the block exists, replace it.

   ```markdown
   ## Agent workflow

   This project uses the `forge` skill. Its settings are in `.agents/forge.md`. The owner starts it with
   `forge <command>`. Do not start it without the owner.
   ```

4. Read `<forge>/reference/tracker-<tracker>.md` for the selected tracker.
5. Tracker `github`: ask the owner first. Then create the labels that do not exist: `needs-owner`, `bug`,
   `enhancement`, and for the full process `milestone`.
6. Tracker `local`: create the directory `.agents/issues/`.
7. Full process: ask the owner if you can create the Roadmap issue and the Backlog issue. Create them as the tracker
   file tells. Write their references into the settings.

## 5. Done

Tell the owner:

- What you wrote and created, and what you propose but did not do (for example, a check script).
- To commit the setup files (`.agents/forge.md`, `.gitignore`, the project instructions) on the default branch before
  the first `forge run`. Worktrees start from the last commit, so they do not have files that are not committed.
- The next command: `forge file` or `forge run` for the light process, or `forge plan` for the full process.
- That they can edit `.agents/forge.md` directly.
