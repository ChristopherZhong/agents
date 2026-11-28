---
name: create-merge-request
description: Creates a GitLab merge request for the current branch with glab after checking branch state, included commits, diff summary, and existing open merge requests.
---

# Create merge request

Create a merge request for the current branch. Follow the repository branch
rules. Never commit or push on a protected branch.

This skill is part of an optional GitLab bundle. Install the bundle only when
the repository uses GitLab.

## Who runs this skill

The `gitlab-specialist` agent, or the user manually. A coordinator can delegate
the work to `gitlab-specialist`. A plan that names this skill does not authorize
the coordinator to run merge-request writes inline.

## Prerequisites

- Run `.agents/skills/verify-gitlab-auth/SKILL.md` first.
- Read `.agents/references/gitlab-conventions.reference.md` for the project
  path, the default branch, the protected branches, and the merge-request
  template.
- Read the project values from the repository project profile or the user. Do
  not guess.

## Workflow

1. Authorize with `verify-gitlab-auth`. Stop when it fails.
1. Verify the working tree and the branch tracking.
1. Summarize what the merge request will include. Compare the branch with the
   default branch.
1. Derive an issue key from the branch only when the branch clearly contains
   one. Otherwise ask the user or write `N/A`.
1. When an issue key is available, obtain the issue context from the user or
   from a parent that uses `jira-specialist`. Do not call Jira from this skill.
1. When the branch is not pushed, check its name. Stop when it is a protected
   branch. Otherwise push the source branch only when the user asked to create
   or push the merge request.
1. List open merge requests for the source branch. Return an existing URL
   instead of creating a duplicate.
1. Read the merge-request template and fill it with the issue key, the branch
   summary, and the test plan.
1. Create the merge request against the default branch unless the user
   specifies another target.
1. Return the merge-request URL. Report the exact failing command when `glab`
   fails.

## Template

Use `.agents/skills/create-merge-request/merge-request-template.md` unless the
repository or the user provides a more specific template.

Include `closes <issue>` only when the merge request fully resolves the
associated issue. Omit the line for partial, preparatory, or follow-up work.

## Quality bar

- Do not push a protected branch.
- Do not create a duplicate merge request.
- Keep the test plan honest. Say what ran, or say that no automated tests ran.
