# Review Jira Issue Prompt

Review a PRD or EDD in Jira for gaps, ambiguities, and inconsistencies.

Workflow reference:

- `.agents/skills/review-jira-issue/SKILL.md`

Requirements:

- Read `.agents/references/jira-conventions.reference.md` first.
- Delegate every Jira fetch and apply to `jira-specialist`.
- Confirm the issue before the review starts.
- Ask the user which document type to review when the labels or body are
  ambiguous.
- Use `.agents/skills/conduct-interview/SKILL.md` in specification review mode.
- Resolve one item at a time. Do not print the internal backlog.
- Ground the review in verified repository paths and versions.

Output format:

1. The resolved decisions
1. The deferred items, when any
1. The proposed Jira changes
