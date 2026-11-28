---
name: create-jira-issue
description: Creates a Jira issue through Atlassian MCP after discovering project fields, and optionally routes the issue to triage or PRD and EDD enrichment.
---

# Create Jira issue

Create an issue, then optionally triage it and enrich it. Follow
`.agents/references/jira-conventions.reference.md` for project values, field
discovery, labels, and body rules.

This skill is part of an optional Jira bundle. Install the bundle only when the
repository uses Jira.

## Who runs this skill

The `jira-specialist` agent, or the user manually. A coordinator can delegate
the work to `jira-specialist`. A plan that names this skill does not authorize
the coordinator to run Jira writes inline.

## Prerequisites

- Run `.agents/skills/verify-jira-auth/SKILL.md` first.
- MCP must pass, because the description is a formatted body.
- Read the site, cloud ID, project key, and issue type names from the repository
  project profile or from the user. Do not guess.
- Read `.agents/references/jira-conventions.reference.md`.

## Workflow

1. Authorize with `verify-jira-auth`. Stop when it fails.
1. Resolve the project values. Ask the user for a missing project key, issue
   type, epic, or component. Do not guess.
1. Resolve the field IDs from issue-type metadata.
1. Draft a concise summary and an initial scope.
1. Create the issue with MCP.
1. Return the issue key and the browse link.

## Field discovery

Epic links and custom fields differ by Jira configuration.

1. List the project issue types.
1. Read the fields for the selected issue type.
1. Find the epic link field, the components, and any required custom field.
1. Use the discovered field ID in the create payload.

Do not hard-code a field ID. Do not create a trial issue to test a field. Do not
probe component names with trial issues. Read the allowed values instead.

## Create payload

| Parameter | Notes |
|---|---|
| Cloud ID | From the auth pre-check |
| Project key | From the project profile or the user |
| Issue type | From the project profile or the user |
| Summary | Concise, no document-type prefix |
| Description | Initial scope, markdown format |
| Additional fields | Epic link and components when needed |

## Optional triage

When the user asks to size the issue, read and follow
`.agents/skills/triage-jira-issue/SKILL.md`.

## Optional enrichment

When the user asks for a PRD or an EDD, read and follow
`.agents/skills/enrich-jira-issue/SKILL.md`. That skill owns the document
structure through `.agents/skills/create-prd/SKILL.md` or
`.agents/skills/create-edd/SKILL.md`.

Do not invent an alternate template.

## Quality bar

- Prefer a discovered field ID over a hard-coded value.
- Prefer a verified path and a verified version over a guess.
- Do not run git commands, migrations, or service operations unless the user
  explicitly asks.

## Related

- `.agents/skills/verify-jira-auth/SKILL.md`
- `.agents/skills/triage-jira-issue/SKILL.md`
- `.agents/skills/enrich-jira-issue/SKILL.md`
- `.agents/skills/review-jira-issue/SKILL.md`
- `.agents/references/jira-conventions.reference.md`
