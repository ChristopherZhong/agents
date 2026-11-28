# Triage Jira Issue Prompt

Estimate delivery effort and assess readiness for a Jira issue.

Workflow reference:

- `.agents/skills/triage-jira-issue/SKILL.md`

Requirements:

- Read `.agents/references/jira-conventions.reference.md` first.
- Run `.agents/skills/verify-jira-auth/SKILL.md` when Jira is used.
- Ground the estimate in repository paths, counts, and configuration.
- Separate technical risk from delivery cost.
- Give the assumptions and a range. Avoid false precision.
- Check PRD or EDD readiness against the core template.
- Merge labels. Never drop an unrelated label.
- Do not imply that implementation is complete.

Output format:

1. The effort range and assumptions
1. The readiness verdict and reason
1. The proposed Jira update
