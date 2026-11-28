# Create Jira Issue Prompt

Create a Jira issue from the requested scope.

Workflow reference:

- `.agents/skills/create-jira-issue/SKILL.md`

Requirements:

- Read `.agents/references/jira-conventions.reference.md` first.
- Run `.agents/skills/verify-jira-auth/SKILL.md` before any Jira call.
- Resolve the project key, issue type, epic, and components from the project
  profile or the user. Do not guess.
- Discover field IDs from issue-type metadata.
- Merge labels. Never drop an unrelated label.
- Do not create a trial issue to test a field.

Output format:

1. The issue key and browse link
1. The fields and labels that were set
1. Any value that the user must confirm
