---
name: update-merge-request
description: Refreshes an existing GitLab merge request body with glab after new commits, aligning the summary, issue reference, and test plan with the branch.
---

# Update merge request

Refresh a merge request after new commits are pushed. Keep the body aligned with
the branch. Keep the test plan and the issue context accurate.

This skill is part of an optional GitLab bundle. Install the bundle only when
the repository uses GitLab.

## Who runs this skill

The `gitlab-specialist` agent, or the user manually. A coordinator can delegate
the work to `gitlab-specialist`.

## Prerequisites

- Run `.agents/skills/verify-gitlab-auth/SKILL.md` first.
- Read `.agents/references/gitlab-conventions.reference.md` for the project
  path, the default branch, and the template.

## Workflow

1. Authorize with `verify-gitlab-auth`. Stop when it fails.
1. Identify the merge-request IID from the user, the current branch, or a
   remote view.
1. Fetch the latest source branch without pushing.
1. Verify the branch state and summarize the remote branch against the default
   branch.
1. View the current merge-request body.
1. Derive an issue key from the branch only when the branch clearly contains
   one. Otherwise keep the existing value, ask the user, or write `N/A`.
1. When an issue key is available, obtain the issue context from the user or
   from a parent that uses `jira-specialist`. Do not call Jira from this skill.
1. Compare the current body with the latest commits, the diff, and the issue.
   Update only when the summary, issue, closing line, or test plan is stale,
   incomplete, or misleading.
1. Use the template at
   `.agents/skills/create-merge-request/merge-request-template.md` unless the
   merge request already has a more specific project template.
1. Update the body.
1. Verify the update with a fresh view.

## Update rules

- Do not commit or push on a protected branch.
- Push a non-protected branch only when the user explicitly asked to push.
- Preserve useful existing details that still apply.
- Add bullets for meaningful new commits. Do not rewrite the whole body for a
  small edit.
- Keep the issue line accurate.
- Include `closes <issue>` only when the merge request fully resolves the
  issue.
- Keep the test plan honest.

## Output

Return the merge-request URL and summarize what changed. When no update is
needed, say that the body is already aligned and return the URL.
