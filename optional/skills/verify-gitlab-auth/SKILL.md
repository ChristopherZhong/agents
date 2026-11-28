---
name: verify-gitlab-auth
description: Verifies GitLab authorization through GitLab MCP or the glab CLI before any merge-request or API operation, and stops on a failed check.
---

# Verify GitLab authorization

Run this before any GitLab API call, including `glab mr`, `glab api`, or a GitLab
MCP tool. Do not continue until authorization passes.

This skill is part of an optional GitLab bundle. Install the bundle only when
the repository uses GitLab.

## When to run

- Always before a skill that creates, updates, lists, or merges a merge request.
- Always before review I/O that fetches a merge request or posts a note.
- Skip only when the parent uses local git fetch and diff with no GitLab API
  call and posts no note.

## Pre-check, in order

### 1. GitLab MCP

1. Confirm that the GitLab MCP server is enabled in the agent harness.
1. Call a lightweight read tool. Scope the call to the project when the tool
   supports a project filter.
1. Pass when the call succeeds without an auth error.
1. Fail when the server is unavailable, a tool is missing, or the call returns
   an auth error. Do not retry the same operation in a loop.

When OAuth is incomplete, tell the user to complete authorization in the
harness. Site administrators may need to approve the application first.

### 2. GitLab CLI

```bash
$ glab auth status
```

- Pass when the output shows an authenticated session for the expected host and
  a token.
- Fail when `glab` is missing, the session is absent, or the command errors.

When the session is absent, tell the user to run:

```bash
$ glab auth login
```

### 3. Token fallback

When the CLI status fails but a token may be configured in the environment,
probe it:

```bash
$ glab api user
```

- Pass when the command returns the current user without an auth error.
- Fail when it reports an unauthorized error.

Direct the user to create a token with the `api` scope and either log in with
it or export it.

## On failure

Stop. Do not continue with a GitLab create, list, update, comment, or merge
operation. Reply with:

1. What failed.
1. How to fix it.
1. A request for confirmation after the user completes authorization.

## On success

- State the path that succeeded.
- Record the host and the authenticated user when available.
- Continue the parent workflow.

## Notes

- MCP and CLI authentication are independent. Either path is sufficient for an
  API or merge-request operation.
- Prefer MCP when the parent workflow uses MCP tools. Prefer `glab` for
  merge-request work.
- A git push or fetch may use separate credentials. This skill validates API
  access, not every remote git operation.
- This skill does not create, edit, or merge a merge request. It only validates
  access.
