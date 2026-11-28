# Jira Conventions

Reusable Jira conventions for the optional Jira bundle. Load this file before
you create, enrich, triage, review, or update an issue with the Jira skills.

This file does not name a site, a project key, or an organization. The
repository supplies those values.

## Project values

Read the repository project profile from `.agents/context/` when it exists. Ask
the user when a value is missing. Do not guess.

| Value | Used for |
|---|---|
| Site hostname | Browse links and MCP resource lookup |
| Cloud ID | Atlassian MCP calls |
| Project key | Issue creation and JQL |
| Issue type names | Task, Story, Bug, and other configured types |
| Epic link field ID | Issue roll-up |
| Component IDs | Component assignment |
| PRD and EDD labels | Document type detection |
| Readiness label | Implementation gate |

Record these values once in a durable context note. Do not repeat them in every
skill.

## Authorization

Run `.agents/skills/verify-jira-auth/SKILL.md` before any Jira read or write.
Stop when authorization fails. Do not retry the same call in a loop.

## MCP and CLI

Use Atlassian MCP when it is available.

- MCP is required for a formatted `description` or a markdown comment.
- A CLI is acceptable for reads, authentication checks, JQL, labels, issue type,
  and a plain summary.
- A CLI that stores markdown as escaped plaintext is not a fallback for a
  formatted body. Do not accept `\#` or `\*\*` in a stored description.

After a body write, fetch the issue again with a markdown or ADF response format.
If escaped markdown is present, rewrite the body through MCP.

Known converter gaps:

| Markdown input | Common stored result | Fix |
|---|---|---|
| Task-list checkboxes | Bullets with a literal `[ ]` | Use an ADF task list |
| A table with an empty header row | Broken or missing header | Give the table a real header row |
| Italic text that contains a backtick | Italic stops at the first backtick | Do not wrap code in italics |

## Field discovery

Discover field IDs from issue-type metadata. Do not guess.

1. List the project issue types.
1. Read the fields for the selected issue type.
1. Find the epic link field, components, and any required custom field.
1. Use the field ID in the create or edit payload.

Do not create a test issue to discover a field or a component. Do not probe
component names with trial creates.

## Labels

An edit replaces the whole label array. Always read the current labels, merge
the requested labels, and deduplicate. Never drop an unrelated label.

Useful labels:

- `PRD` — the issue body is a product requirements document.
- `EDD` — the issue body is an engineering design document.
- `ready-to-implement` — the issue passed the readiness check.

## Issue types and summaries

Follow the document type:

| Document | Issue type | Label | Summary |
|---|---|---|---|
| PRD | Story, or the project equivalent | `PRD` | Product-facing summary |
| EDD | Task, or the project equivalent | `EDD` | Engineering-facing summary |

Do not add a `[PRD]` or `[EDD]` prefix to the summary. Use a domain tag only
when the repository defines one.

## Readiness

Use `ready-to-implement` only when all are true:

- The body is a complete PRD or EDD for its template.
- The internal gap backlog is empty.
- The open-questions section is absent, empty, or states that there are none.

Remove the label when the issue is not ready, lacks a PRD or EDD, or readiness
was not assessed.

## Issue keys in branches

A branch may embed an issue key. Treat the key as optional. Infer it only when
the branch name clearly contains one, such as `feature/ABC-123`. Otherwise ask
the user. Do not invent a key.

## Related standards

- Write prose in ASD-STE100. Read `.agents/references/asd-ste100.reference.md`.
- Write behavioral requirements in EARS. Read
  `.agents/references/ears.reference.md`.
- Use `.agents/skills/create-prd/SKILL.md` and
  `.agents/skills/create-edd/SKILL.md` for document structure.
