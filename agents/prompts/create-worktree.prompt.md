# Create Worktree Prompt

Create or reuse a git worktree for a branch.

Workflow reference:

- `.agents/skills/create-worktree/SKILL.md`

Requirements:

- Use the branch, base ref, and reuse policy that the user or repository policy
  provides.
- Check the registered worktrees and branch location before creating anything.
- Stop and ask when a path, branch, or base ref conflicts.
- Prepare only the setup steps that the repository documents.
- Do not copy secrets, remove worktrees, delete branches, start services, commit,
  or push.

Output format:

1. Branch
1. Worktree path
1. Created or reused
1. Base ref
1. Blockers or user decisions
