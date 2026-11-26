# Tracker: local

Issues are Markdown files in `<main checkout>/.agents/issues/<NNN>-<slug>.md` (`<NNN>` is the next zero-padded 3-digit number, e.g., `012`). Always reference issues by `<NNN>` and always use `<main checkout>` in paths (uncommitted issue files do not exist in worktrees). A "PR" is a branch plus a `## Pull request` section in the issue file.

Only the orchestrator modifies issue files. Commit `.agents/issues/` on the default branch during merges and when committing approved `kickoff`/`roadmap`/`plan` outputs.

## File format

```markdown
# <title>

Status: open | closed
Labels: <label>, <label>
Parent: <NNN> | none
Branch: <branch> | none

<body: issue spec>

## Pull request

<PR text from implementer>

## Comments

### <date> <role> (<model>)
<comment>
```

## Actions

| Action | How |
| --- | --- |
| Find issues | `grep -rliE "<word>\|<word>" <main checkout>/.agents/issues/` |
| List open issues by label | `grep -lE "^Labels:.*\b<label>\b" <main checkout>/.agents/issues/*.md` filtered to `Status: open` |
| Read an issue | Read the file. |
| List child issues | `grep -l "^Parent: <NNN>$" <main checkout>/.agents/issues/*.md` |
| Create an issue | Create `<NNN>-<slug>.md` with `Status: open`. |
| Edit an issue body | Replace body only; preserve `## Pull request` and `## Comments`. |
| Comment on an issue | Append a new `### <date> <role> (<model>)` entry under `## Comments`. Never edit earlier comments. |
| Add / remove label | Edit the `Labels:` line. |
| Close an issue | Append closing comment and set `Status: closed`. |
| Open a PR | Set `Branch: <branch>` and write PR text under `## Pull request`. |
| Update a PR | Implementer commits (and pushes if remote exists) on `<branch>`; update `## Pull request` if text changed. |
| Read a PR & diff | Read `## Pull request` and run `git diff <default branch>...<branch>`. |
| Check out a PR | Temporary detached worktree: `git worktree add --detach <tmp> <branch>`. Clean up: `git worktree remove <tmp>`. |
| Comment on a PR | Append comment to the issue prefixed with `Pull request:`. |
| Merge a PR | In `<main checkout>` on the default branch: (1) `git merge --squash <branch>`, (2) append the closing comment and set `Status: closed`, (3) `git add` the issue file and any other issue files modified by this run, (4) `git commit -s` referencing the issue title and `<NNN>`, (5) delete the branch (local + remote if pushed), (6) push default branch if remote exists. |
| Delete a branch (spikes) | `git branch -D <branch>` and `git push origin --delete <branch>` (if pushed). |

- `Closes` lines are no-ops here; the merge step closes the issue before committing.
