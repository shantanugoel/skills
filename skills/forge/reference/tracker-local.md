# Tracker: local

Issues are Markdown files in the repository. There is no server. A "pull request" is a branch and a section in the
issue file.

## Files

- Each issue is one file: `<main checkout>/.agents/issues/<NNN>-<slug>.md`. `<NNN>` is the next free number, with
  three digits, for example `012`. An issue reference is always these three digits. Use them in each "Parent" line,
  each "Needs" line and each comment.
- `<main checkout>` is the absolute path of the main checkout of the repository. Use it in each path. A worktree does
  not have the issue files that are not committed yet.
- Only the orchestrator and the commands change issue files. A subagent reads the issue file, and sends back its
  comments and its pull request text. The orchestrator writes them into the file.
- The orchestrator commits the issue files on the default branch, in the same commit as a merge. Before that, they
  are changes in the main checkout that are not committed.

An issue file has this form:

```
# <title>

Status: open | closed
Labels: <label>, <label>
Parent: <NNN> or none
Branch: <branch> or none

<body: the spec, in the form of the planner role>

## Pull request

<the pull request text of the implementer, when the build is done>

## Comments

### <date> <role> (<model>)
<comment>
```

## Actions

| Action | How |
| --- | --- |
| Find issues | `grep -rliE "<word>\|<word>" <main checkout>/.agents/issues/` |
| List open issues with a label | `grep -lE "^Labels:.*\b<label>\b" <main checkout>/.agents/issues/*.md`, then keep the files with `Status: open` |
| Read an issue | Read the file. |
| List the children of an issue | `grep -l "^Parent: <NNN>$" <main checkout>/.agents/issues/*.md` |
| Create an issue | Write a new file with the next free number. Set `Status: open`. |
| Edit the body of an issue | Change the body. Do not change the "Comments" section. |
| Comment on an issue | Add a comment at the end of the "Comments" section. Do not change an earlier comment. |
| Add or remove a label | Change the "Labels" line. |
| Close an issue | Add a comment with the reason, and set `Status: closed`. |
| Open a pull request | The implementer commits on the branch, and sends back the branch and the pull request text. The orchestrator sets the "Branch" line and writes the text in the "Pull request" section. |
| Update a pull request | Commit on the same branch. |
| Read a pull request | Read the "Pull request" section. Read the diff: `git diff <default branch>...<branch>`. |
| Check out a pull request | In a temporary worktree, not in the main checkout: `git worktree add --detach <tmp> <branch>`. Remove it when you are done: `git worktree remove <tmp>`. |
| Comment on a pull request | Comment on the issue. Start the comment with "Pull request:". |
| Merge a pull request | In the main checkout, on the default branch: (1) `git merge --squash <branch>`. (2) Close the issue. (3) `git add` the issue file, and each other issue file that this run changed. (4) `git commit -s` with the title and the reference of the issue. (5) `git branch -D <branch>`. |

- If the repository has a remote, push the branch and the default branch as usual.
- "Closes" lines do nothing here. Close the issue yourself during the merge.
