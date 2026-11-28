---
name: verify-jira-auth
description: Verifies Jira authorization through Atlassian MCP or a Jira CLI before any issue read or write, and stops when a formatted body cannot be written safely.
---

# Verify Jira authorization

Run this before any Jira API call, including issue fetch, create, edit, comment,
or JQL search. Do not guess a cloud ID or a site. Do not continue until
authorization passes.

This skill is part of an optional Jira bundle. Install the bundle only when the
repository uses Jira.

## When to run

- Always before a skill that creates, fetches, enriches, triages, or updates a
  Jira issue.
- Always before review I/O that fetches or applies issue changes.
- Skip only when the parent uses a pasted document and makes no Jira call.

## Pre-check, in order

### 1. Atlassian MCP

1. Call the resource discovery tool.
1. Pass when the call returns at least one resource with a cloud ID or an ID and
   a Jira site URL.
1. Record the cloud ID and the site hostname for later steps.
1. Fail on an auth error, an incomplete OAuth flow, an empty resource list, or a
   missing tool. Do not retry the same operation in a loop.

When MCP fails and the workflow must write a formatted `description` or a
markdown comment, do not fall through to a CLI. Treat the write as blocked and
tell the user to complete MCP authorization.

### 2. Atlassian CLI

Use this only when MCP is unavailable and the work is read-only or does not
write a formatted body.

```bash
$ acli jira auth status
```

- Pass when the command reports an authenticated session for the expected site.
- Fail when the CLI is missing, the session is absent, or the command errors.

When the session is absent, tell the user to run:

```bash
$ acli jira auth login --web
```

### 3. Community Jira CLI

Use this only when the environment clearly provides a community `jira` CLI.

```bash
$ jira me
```

- Pass when the command returns the current user without an auth error.
- Fail when the binary is missing or reports an unauthorized error.

Direct the user to the CLI's own setup procedure when it fails.

## On failure

Stop. Do not continue with any Jira create, fetch, or edit. Reply with:

1. What failed.
1. How to fix it. Use MCP authorization for a formatted body. Use MCP or a CLI
   for a read.
1. A request for confirmation after the user completes authorization.

## On success

- State the path that succeeded.
- Record the cloud ID and the site hostname.
- Continue the parent workflow.

## Notes

- MCP and CLI authentication are independent.
- A read may use either path. A formatted body write requires MCP.
- This skill does not create, edit, or fetch an issue. It only validates access.
