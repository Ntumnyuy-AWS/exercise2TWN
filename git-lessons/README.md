# Git & Version Control — Lesson 1

## Objective

Understand how Git tracks changes and how to save and share
work using commits, branches, and remote repositories.

## The Git Workflow

1. Working directory: create or modify files.
2. Staging area: select changes with `git add`.
3. Local repository: save a snapshot with `git commit`.
4. Remote repository: publish commits with `git push`.

## Essential Commands

| Command | Purpose |
|---|---|
| `git status` | Inspect the working tree and branch |
| `git add` | Stage changes for a commit |
| `git diff` | Inspect unstaged changes |
| `git diff --staged` | Inspect staged changes |
| `git commit` | Save staged changes in local history |
| `git log --oneline` | Review commit history |
| `git push` | Publish commits to a remote |
| `git branch` | List local branches |

## Branching

Branches allow changes to be developed separately from other work.

The branch `feature/gitlessons` is being used to practise
Git commands without directly modifying the networking branch.

## Practical Git Workflow Completed

- Created a feature branch.
- Created and edited a README with Vim.
- Staged and committed the new file.
- Pushed the branch to GitHub.

## Key Takeaway

Git commits record changes locally. Pushing sends those commits
to a remote repository such as GitHub.

