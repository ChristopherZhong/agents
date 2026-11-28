# GitLab Conventions

Reusable GitLab conventions for the optional GitLab bundle. Load this file
before you create, update, review, or query a merge request with the GitLab
skills.

This file does not name a host, a project path, or an organization. The
repository supplies those values.

## Project values

Read the repository project profile from `.agents/context/` when it exists. Ask
the user when a value is missing. Do not guess.

| Value | Used for |
|---|---|
| GitLab host | Authentication and browse links |
| Project path | API calls and merge-request links |
| Default branch | Branch checks and diff base |
| Protected branches | Push and merge guards |
| Merge-request template | Merge-request body structure |
| Dependency installer | Local dependency refresh after checkout |

Record these values once in a durable context note. Do not repeat them in every
skill.

## Authorization

Run `.agents/skills/verify-gitlab-auth/SKILL.md` before any GitLab API call.
Stop when authorization fails. Do not retry the same call in a loop.

## MCP and CLI

Use `glab` for merge-request work when it is available. Use GitLab MCP when the
workflow is MCP-oriented or `glab` is unavailable.

Do not invent MCP tool names. Inspect the enabled tool list first.

## Merge-request body

Use the template at
`.agents/skills/create-merge-request/merge-request-template.md` unless the
repository provides a more specific template.

- State the issue key when one exists. Write `N/A` when none exists.
- Summarize behavior, documentation, or workflow changes.
- List the validation commands that actually ran.
- Say plainly when no automated tests ran.
- Include `closes <issue>` only when the merge request fully resolves the issue.

## Branch and push safety

- Never commit or push on a protected branch.
- Push a source branch only when the user asked to create or update the merge
  request.
- Never force-push.
- Do not run database migrations or start services during a review.

## Duplicate merges

List open merge requests for the source branch before you create one. Return the
existing URL instead of creating a duplicate.

## Review I/O

The reviewer judges the diff. The GitLab specialist fetches data and posts the
review.

Fetch:

- Merge-request metadata and description.
- Source and target branches, and the commit SHAs.
- The full diff.
- Existing notes and unresolved resolvable discussions.
- The latest pipeline status.

Post:

- Delete an earlier agent review note before posting a replacement. Match the
  review heading, not an arbitrary note.
- Resolve only the discussion IDs that the reviewer listed.
- Post inline comments that the reviewer wrote. Do not rewrite them.
- Post the reviewer's complete markdown as one note.

Filter system notes and already-resolved threads out of the fetch payload.

## Review note shape

Use one stable heading so a later run can find and replace its own note. Keep
the traffic light, checklist, and recommendation sections.

## Related standards

- Use `.agents/skills/verify-gitlab-auth/SKILL.md` before GitLab I/O.
- Use `.agents/skills/create-merge-request/SKILL.md` to create a merge request.
- Use `.agents/skills/update-merge-request/SKILL.md` to refresh a body.
- Use `.agents/skills/review-merge-request/SKILL.md` to judge a diff.
