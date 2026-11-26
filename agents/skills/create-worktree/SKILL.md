---
name: create-worktree
description: Creates or reuses a git worktree for a branch, checks for conflicts, and moves work into it. Use when the user asks for a worktree or repository policy requires one.
---

# Create Worktree

Create or reuse a worktree without touching the current checkout. This skill
does not remove worktrees, delete branches, start services, commit, or push.

User-facing prompt reference:

- `.agents/prompts/create-worktree.prompt.md`

## Inputs

- **Branch** (required). Use the branch name that the task or repository policy
  asks for.
- **Base ref** for a new branch. Default to the repository integration branch.
- **Reuse allowed**. Use true for a resumable workflow branch and false for a
  new task branch.

## Resolve paths

Run:

```bash
git worktree list --porcelain
```

- Primary checkout: the first `worktree` entry.
- Worktree path:
  `<parent-of-primary>/<primary-basename>.worktrees/<branch with "/" replaced by "-">`.

Example: for primary checkout `/work/app` and branch `fix/login`, use
`/work/app.worktrees/fix-login`.

When the base ref is not provided, resolve the integration branch with
`git symbolic-ref --quiet --short refs/remotes/origin/HEAD` and remove the
`origin/` prefix. If the command fails, ask for the base ref.

## Workflow

1. Resolve the primary checkout and the worktree path.
1. Check for conflicts. Stop and ask the user when:
   - The worktree path exists but is not a registered worktree.
   - The branch is checked out in another worktree. Report that path.
   - The branch exists and reuse is not allowed.
1. Create or reuse the worktree:
   - Path already registered for this branch and reuse allowed: reuse it. Do not
     run another create command.
   - Local branch exists: `git worktree add <path> <branch>`.
   - Branch exists only on the remote: `git fetch origin <branch>`, then
     `git branch --track <branch> origin/<branch>`, then
     `git worktree add <path> <branch>`.
   - Branch does not exist: `git fetch origin <base>`, then
     `git branch --track <branch> origin/<base>`, then
     `git worktree add <path> <branch>`.
1. Prepare the worktree:
   - Run only the setup steps that the repository documents.
   - Link or create environment files only when the repository documents it.
     Never copy secrets.
   - Install dependencies only when they are missing and the repository
     documents the install command.
1. Move work into the worktree:
   - Use the worktree as the working directory for later commands.
   - Edit files only by absolute paths under the worktree.
   - Do not edit the primary checkout.
1. Report the branch, the path, whether it was created or reused, and the base
   ref.

## Cleanup

- Do not remove a worktree unless the user asks.
- Before removal, run `git status --short` in the worktree. Stop when it has
  changes.
- Remove only after approval: `git worktree remove <path>`.
- Do not use `--force` without explicit approval.
- Do not delete the branch unless the user asks.

## Safety

- Do not run destructive git commands.
- Do not start, stop, or restart services.
- Do not commit or push.
- Stop when a path, branch, or base ref is ambiguous.
