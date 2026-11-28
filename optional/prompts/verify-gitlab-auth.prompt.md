# Verify GitLab Auth Prompt

Verify GitLab authorization before any merge-request or API operation.

Workflow reference:

- `.agents/skills/verify-gitlab-auth/SKILL.md`

Requirements:

- Try GitLab MCP first when the workflow uses MCP tools.
- Use `glab auth status` for the CLI path.
- Probe a configured token only when the stored session fails.
- Report the exact failure and the fix.
- Do not retry the same call in a loop.

Output format:

1. The path that succeeded or failed
1. The host and user when the check passes
1. The user action that is required when the check fails
