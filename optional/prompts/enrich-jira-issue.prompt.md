# Enrich Jira Issue Prompt

Expand a Jira issue as a PRD or an EDD.

Workflow reference:

- `.agents/skills/enrich-jira-issue/SKILL.md`

Requirements:

- Read `.agents/references/jira-conventions.reference.md` first.
- Run `.agents/skills/verify-jira-auth/SKILL.md` before any Jira call.
- Ask which document type to use when the request is unclear.
- Follow `.agents/skills/create-prd/SKILL.md` or
  `.agents/skills/create-edd/SKILL.md` for structure.
- Apply STE to prose and EARS to behavioral requirements.
- Ground the draft in repository paths and versions.
- Merge labels. Never drop an unrelated label.
- Fetch the body after the write and reject escaped markdown.

Output format:

1. The issue key and browse link
1. The document type and label
1. The fields and labels that changed
1. Any open question that remains
