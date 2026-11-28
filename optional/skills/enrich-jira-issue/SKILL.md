---
name: enrich-jira-issue
description: Enriches a Jira issue by composing the core PRD or EDD workflow, then applying Jira labels, summary, and issue type through Atlassian MCP.
---

# Enrich Jira issue

Expand an existing issue as a product requirements document or an engineering
design document.

This skill is part of an optional Jira bundle. Install the bundle only when the
repository uses Jira.

## Composition

The document structure belongs to the core skills.

- For a PRD, read `.agents/skills/create-prd/SKILL.md` and
  `.agents/skills/create-prd/prd-template.md`.
- For an EDD, read `.agents/skills/create-edd/SKILL.md` and
  `.agents/skills/create-edd/edd-template.md`.
- Read `.agents/references/asd-ste100.reference.md` for prose.
- Read `.agents/references/ears.reference.md` for behavioral requirements.
- Read `.agents/references/jira-conventions.reference.md` for labels, issue
  types, summaries, and body writes.

Do not duplicate a template here. Follow the selected core skill.

When the document type is unclear, ask the user before drafting.

When the user asks to review an existing PRD or EDD for gaps, stop and return to
the parent. The parent runs `.agents/skills/review-jira-issue/SKILL.md` and
delegates Jira fetch and apply back to this agent. Do not start an interview
here.

## Prerequisites

- Run `.agents/skills/verify-jira-auth/SKILL.md` first.
- MCP must pass, because the description is a formatted body.
- Read the site and cloud ID from the project profile or the user.
- Do not enrich through a CLI that stores markdown as escaped plaintext.

## Workflow

1. Authorize with `verify-jira-auth`. Stop when it fails.
1. Parse the issue key.
1. Fetch the issue. Read at least the summary, description, labels, issue type,
   parent, project, and status.
1. Choose the document type. Load the core PRD or EDD skill.
1. Ground the draft in the repository when the issue concerns this repository.
   Read paths and versions. Do not guess.
1. Draft the description in markdown with the selected core skill.
1. Merge the labels. Add `PRD` or `EDD`. Keep unrelated labels.
1. Edit the issue with MCP. Set the description, the improved summary, the
   merged labels, and the issue type that the core skill requires.
1. Fetch the issue again. Reject escaped plaintext. Rewrite a broken body as
   ADF when the converter drops a task list or a table header.
1. Reply with the browse link and a short change summary.

## Quality bar

- The core skill owns the template and the document semantics.
- This skill owns Jira orchestration and repository grounding.
- Use verified paths and versions only.
- Do not run git commands, migrations, or service operations unless the user
  explicitly asks for implementation work.

## Related

- `.agents/skills/verify-jira-auth/SKILL.md`
- `.agents/skills/create-jira-issue/SKILL.md`
- `.agents/skills/review-jira-issue/SKILL.md`
- `.agents/skills/create-prd/SKILL.md`
- `.agents/skills/create-edd/SKILL.md`
- `.agents/references/jira-conventions.reference.md`
