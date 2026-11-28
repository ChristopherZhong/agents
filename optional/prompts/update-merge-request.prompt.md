# Update Merge Request Prompt

Refresh an existing GitLab merge request body after new commits.

Workflow reference:

- `.agents/skills/update-merge-request/SKILL.md`

Requirements:

- Read `.agents/references/gitlab-conventions.reference.md` first.
- Run `.agents/skills/verify-gitlab-auth/SKILL.md` before any GitLab call.
- Compare the body with the latest commits, the diff, and the issue.
- Update only a stale, incomplete, or misleading section.
- Preserve useful existing details.
- Keep the test plan honest.

Output format:

1. The merge-request URL
1. The sections that changed
1. A statement when the body is already aligned
