# Review Merge Request Prompt

Perform an initial review of a GitLab merge request.

Workflow reference:

- `.agents/skills/review-merge-request/SKILL.md`

Requirements:

- Read `.agents/references/gitlab-conventions.reference.md` first.
- Delegate every GitLab fetch and post to `gitlab-specialist`.
- Keep the review read-only. Do not commit, push, merge, or run migrations.
- Judge the diff against the project conventions.
- Include the traffic light every time.
- Prepare inline comments but do not post them yourself.
- Resolve only the discussions that the review confirms are fixed.

Output format:

1. The traffic light and reason
1. The checklist and findings
1. The proposed inline comments and discussion resolutions
