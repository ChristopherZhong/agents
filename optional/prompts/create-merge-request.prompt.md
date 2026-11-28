# Create Merge Request Prompt

Create a GitLab merge request for the current branch.

Workflow reference:

- `.agents/skills/create-merge-request/SKILL.md`

Requirements:

- Read `.agents/references/gitlab-conventions.reference.md` first.
- Run `.agents/skills/verify-gitlab-auth/SKILL.md` before any GitLab call.
- Verify the branch state and the included commits.
- Check for an existing open merge request for the source branch.
- Do not push a protected branch.
- Use the merge-request template.
- Keep the test plan honest.

Output format:

1. The merge-request URL
1. The target branch and issue reference
1. The checks that ran, or a statement that no automated tests ran
