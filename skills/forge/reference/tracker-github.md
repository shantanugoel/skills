# Tracker: GitHub

Issues and PRs live on GitHub via `gh`. An issue reference is its number (e.g., `12`). Only the orchestrator performs write actions; subagents may run read actions.

| Action | Command |
| --- | --- |
| Find issues | `gh issue list --state all --search "<words>"` |
| List open issues by label | `gh issue list --state open --label <label>` |
| Read an issue | `gh issue view <n> --json number,title,state,labels,body,comments` |
| List child issues | `gh issue view <n> --json subIssues` |
| Create an issue | Write body to a temp file, then `gh issue create --title "<title>" --body-file <file> [--label <label>] [--parent <n>]` |
| Edit an issue body | `gh issue edit <n> --body-file <file>` |
| Comment on an issue | `gh issue comment <n> --body-file <file>` |
| Add / remove label | `gh issue edit <n> --add-label <label>` / `--remove-label <label>` |
| Close an issue | Comment first, then `gh issue close <n>` (if already closed, only comment). |
| Open a PR | `gh pr create --head <branch> --title "<title>" --body-file <file>` (include `Closes #<issue>`). |
| Update a PR | Implementer pushes new commits to `<branch>`. |
| Read a PR & diff | `gh pr view <n> --json number,title,body,headRefName,comments,reviews` and `gh pr diff <n>` |
| Check out a PR | Temporary detached worktree: `git fetch origin <branch> && git worktree add --detach <tmp> origin/<branch>`. Clean up: `git worktree remove <tmp>`. |
| Comment on a PR | `gh pr comment <n> --body-file <file>` |
| Merge a PR | `gh pr merge <n> --squash --delete-branch` |
| Delete a branch (spikes) | `git branch -D <branch>` (if local) and `git push origin --delete <branch>` (if pushed). |

- If `Repository` is set in `.agents/forge.md`, pass `--repo <owner/name>` to every `gh issue` and `gh pr` command.
- Always pass multi-line Markdown via `--body-file`, never inline shell arguments.
- If a label is missing, create it (`gh label create <label>`) or tell the owner.
- Roadmap, milestones, and backlog are issues—not GitHub Milestones.
