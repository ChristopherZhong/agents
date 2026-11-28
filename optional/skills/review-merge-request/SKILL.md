---
name: review-merge-request
description: Performs an initial GitLab merge-request review with a checklist, a traffic-light merge risk, and a review body posted through a GitLab specialist.
---

# Review merge request

Perform an initial review. Confirm that the core logic is not broken, the change
is coherent, and the tests are adequate. This does not replace human review for
domain judgment or approval.

This skill is part of an optional GitLab bundle. Install the bundle only when
the repository uses GitLab.

## Role split

This skill owns code-review judgment. GitLab API work belongs to
`gitlab-specialist`.

| Context | Judgment | GitLab fetch and post |
|---|---|---|
| Coordinator, parent, or main agent | Yes | No. Delegate to `gitlab-specialist`. |
| `gitlab-specialist` | No | Yes. Return data, post the supplied body, and resolve the listed IDs. |
| User manually | Yes | Yes |
| Any other sub-agent | Yes, when asked | No |

When `gitlab-specialist` is asked to review a merge request without a finished
review body, it fetches and returns data only. It does not write a traffic light
or a checklist review.

## Read-only review

The reviewer must never stage, commit, push, or merge code.

Allowed local git: fetch, checkout to switch branch, status, diff, and log.

Do not run database migrations. Review a migration file by reading it.

Do not call `glab`, `glab api`, `glab ci`, GitLab MCP merge-request tools, or
`verify-gitlab-auth`. Those steps run inside `gitlab-specialist`.

## When to use

- The user asks to review a merge request or to check merge readiness.
- The user gives a merge-request IID or a source branch.

## Prerequisites

- Work from the repository root.
- Read the project path and integration branch from the repository project
  profile or the user.
- Extract the IID from the user request. When the user gives only a source
  branch, delegate a branch lookup to `gitlab-specialist`.
- When a checkout is needed and the working tree is dirty, warn the user and ask
  before switching.

## Workflow

1. Parse the merge-request IID and the branch when given.
1. Fetch context through the GitLab specialist, or use the local git path when
   GitLab I/O is unavailable.
1. Judge the diff with the review process below. Write the review yourself.
1. Show the review to the user.
1. Delegate the post step to `gitlab-specialist`. Skip posting on the local path
   when GitLab I/O is unavailable.

Delegate every GitLab call to `gitlab-specialist`.

### Fetch through the specialist

Ask `gitlab-specialist` to authorize and return data only: title, description,
branches, SHAs, full diff, existing notes, unresolved resolvable discussions,
and the latest pipeline status. Do not ask for a review.

When the fetch fails, stop using GitLab I/O for this review. Use the local path
and ask the user for the branch name when you do not have it.

### Local git path

Use this path when no GitLab I/O is available. It is read-only with respect to
the remote.

1. Get the branch from the user, the GitLab UI, or a remote fetch.
1. Fetch the branch and check it out when appropriate. Warn when the working
   tree is dirty.
1. Diff against the integration branch.

The user can return with a checkout of the previous branch. Do not run a
destructive git command without permission.

## Review process

### 1. Gather context

Read the title, description, and diff from the fetch step, the local diff, the
GitLab UI, or a user paste. When a dependency or schema change is present,
refresh dependencies with the project's documented installer. Do not run
migrations. Ground every claim in a file you can see.

### 2. Core logic and coherence

- Confirm that each changed area is consistent with the existing patterns.
- Look for an obvious regression, such as removed error handling or an inverted
  condition.
- Confirm that the change matches the merge-request summary. Flag unrelated
  edits and unclear scope.
- Check the project rules. Flag forbidden debug output, destructive database
  commands, service restarts, and non-conventional commit messages.
- Check the repository conventions. Follow `AGENTS.md` and the project patterns.

### 3. Inline comments

Prepare line-specific feedback. Do not post it yourself.

Collect a list for `gitlab-specialist`: a repository-relative file path, a
1-based line number, and the comment body.

Include a comment when you find broken code, incorrect logic, a pattern
violation, a security concern on a changed line, or a missing test at the line
that needs coverage.

Do not include architecture, scope, or overall assessment. Those belong in the
main note. Do not comment on a file that the merge request did not change. Do
not add more than about three to five inline comments on one file. Consolidate
the rest into the main note.

Reference the inline comments in the main note.

### 4. Prior discussions

For each unresolved resolvable discussion from the fetch step, decide from the
current head, not from the original comment SHA.

| Decision | When |
|---|---|
| Resolve | You can still identify the same defect and confirm that it is fixed. |
| Leave open | The defect remains, is partly fixed, needs author confirmation, or you did not re-check the thread. |

A missing line is not a fix. Code can move, rename, or inline and still be
wrong. List those threads under author confirmation.

Collect the discussion IDs to resolve. When the fetch returned only a note ID,
pass that ID instead. Include prior agent reviews and other reviewer comments
when you judged them addressed. Do not resolve a system note, an already
resolved thread, or an author-confirmation item.

Do not resolve a discussion yourself. Pass the ID list to `gitlab-specialist`.
Mention what you resolved, or that none qualified, in the main note.

### 5. Tests

- For a code change, confirm that existing tests cover the change or that new
  tests were added.
- When the author says that no unit test change is required, check that the
  reason is sound.
- Check that new tests follow the project test patterns and target the changed
  behavior.
- Do not require tests for a documentation-only or configuration-only change
  that adds no logic.

### 6. Merge-request checklist

Walk through the template and mark each item from the code and content that you
can see, not from the author's checkboxes.

Report each item as pass, fail, not applicable, or unclear.

- Summary: the merge request states what changed and why.
- Unit tests: existing tests cover the change, new tests were added, or the
  reason for no test change is sound.
- External testing: recorded when the repository requires it.
- Database: a migration is called out when present.
- Environment variables: a new variable is documented.
- Security: no secret, key, or credential is present, and security impact is
  considered.
- Pre-merge: the code follows the project conventions, and the change is
  limited to the request.
- CI: note the lint, test, and build status when you can verify it. Otherwise
  ask the author to confirm.

### 7. Traffic light

Always include a traffic-light assessment, even when the checklist passes.

| Light | Meaning | When to use |
|---|---|---|
| RED | The current flow changed significantly. Merge only when that was the intent. | A core path, critical logic, or shared code changed in a way that alters existing behavior. |
| AMBER | Moderate risk. Review carefully. | A critical path or shared code changed narrowly, or the tests are light for the scope. |
| GREEN | Low risk. The change is localized or well covered. | New code or a small edit with good test coverage and no material change to an existing flow. |

State the light and one short reason.

### 8. Output format

Produce a review report in this structure. The traffic light section is
required.

```markdown
# Merge Request Review: [merge request number or title]

## Traffic light (merge risk)

**[RED | AMBER | GREEN]** - [One sentence: why this level and what to do.]

---

## Summary

[One or two sentences on what the merge request does and the overall assessment.]

## Checklist

| Item | Status | Notes |
| --- | --- | --- |
| Summary | Pass, fail, or N/A | |
| Unit tests | | |
| External testing | | |
| Database | | |
| Environment variables | | |
| Security | | |
| Pre-merge conventions and scope | | |
| CI | | |

## Core logic and coherence

[Brief bullets: what was checked, and any concern or regression.]

## Tests

[How tests were addressed, and any gap or suggestion.]

## Recommendations

- **Must fix**: [Anything that must be addressed before merge.]
- **Suggest**: [Optional improvements.]
- **Author to confirm**: [Checks the author must confirm.]
- **Resolved discussions**: [Discussion IDs and a one-line reason, or none.]
```

The traffic light reflects risk to existing flows, not only checklist pass or
fail.

### 9. Post through the specialist

Delegate the post step to `gitlab-specialist`. Do not run `glab mr note`
yourself.

Give the specialist:

1. The merge-request IID.
1. The complete review markdown.
1. The inline comment list.
1. The discussion IDs or note IDs to resolve.
1. The instruction to delete an earlier agent review note first, resolve only
   the listed discussions, post the inline comments, then post the main note.

Skip the post step on the local path when GitLab I/O is unavailable. Still give
the user the full review.

The I/O commands and cleanup details live in
`.agents/references/gitlab-conventions.reference.md`.

## Scope

- In scope: correctness, coherence, tests, and alignment with the merge-request
  template and the project rules.
- Out of scope: domain approval and product decisions.
