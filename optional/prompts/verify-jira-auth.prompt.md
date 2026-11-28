# Verify Jira Auth Prompt

Verify Jira authorization before any issue read or write.

Workflow reference:

- `.agents/skills/verify-jira-auth/SKILL.md`

Requirements:

- Try Atlassian MCP first.
- Use a CLI only for a read or a non-body field.
- Do not fall through to a CLI for a formatted description or a markdown
  comment.
- Report the exact failure and the fix.
- Do not retry the same call in a loop.

Output format:

1. The path that succeeded or failed
1. The cloud ID and site when the check passes
1. The user action that is required when the check fails
