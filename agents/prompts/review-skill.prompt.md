# Review Skill Prompt

Review a skill in `.agents/skills/` before it is kept.

Workflow reference:

- `.agents/skills/review-skill/SKILL.md`

Requirements:

- Check naming, discovery, scope, workflow, consistency, gaps, ambiguity,
  safety, maintainability, and token load.
- Read every support file the skill references.
- Apply High and Medium fixes before reporting completion.
- Keep required steps, safety rules, and trigger phrases intact.

Output format:

1. Findings by severity with file paths
1. Fixes applied
1. Open questions
1. Readiness summary
