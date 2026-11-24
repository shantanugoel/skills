# Tracker: GitHub

Issues and pull requests are on GitHub. Use the `gh` command in the main checkout. An issue reference is a number,
for example `12`.

| Action | How |
| --- | --- |
| Find issues | `gh issue list --state all --search "<words>"` |
| List open issues with a label | `gh issue list --state open --label <label>` |
| Read an issue | `gh issue view <n> --json number,title,state,labels,body,comments` |
| List the children of an issue | `gh issue view <n> --json subIssues` |
| Create an issue | Write the body to a file. `gh issue create --title "<title>" --body-file <file> [--label <label>] [--parent <n>]` |
| Edit the body of an issue | `gh issue edit <n> --body-file <file>` |
| Comment on an issue | `gh issue comment <n> --body-file <file>` |
| Add or remove a label | `gh issue edit <n> --add-label <label>` or `--remove-label <label>` |
| Close an issue | Comment first, then `gh issue close <n>`. If the issue is closed already, only comment. |
| Open a pull request | Push the branch. `gh pr create --head <branch> --title "<title>" --body-file <file>`. Put `Closes #<issue>` in the body. |
| Update a pull request | Push to the same branch. |
| Read a pull request | `gh pr view <n> --json number,title,body,headRefName,comments,reviews` and `gh pr diff <n>` |
| Check out a pull request | In a temporary worktree, not in the main checkout: `git fetch origin <branch>`, then `git worktree add --detach <tmp> origin/<branch>`. Remove it when you are done: `git worktree remove <tmp>`. |
| Comment on a pull request | `gh pr comment <n> --body-file <file>` |
| Merge a pull request | `gh pr merge <n> --squash --delete-branch` |

- If the settings name a "Repository", add `--repo <owner/name>` to each `gh issue` and `gh pr` command.
- Use a file for each body or comment that has more than one line. Do not put Markdown in a shell argument.
- If a label does not exist, create it (`gh label create <label>`) or tell the owner.
- A milestone, the roadmap and the backlog are issues. They are not GitHub milestones.
