---
name: triage-jira-issue
description: Estimates delivery effort and assesses PRD or EDD readiness for a Jira issue, with repository-grounded evidence and an optional Jira update.
---

# Triage Jira issue

Estimate delivery effort and assess readiness. Triage supports prioritization
and sizing. It is not implementation, and it is not a completion gate.

This skill is part of an optional Jira bundle. Install the bundle only when the
repository uses Jira.

## Prerequisites

- Run `.agents/skills/verify-jira-auth/SKILL.md` when the workflow reads or
  writes Jira. Skip it only for repository-only triage with no Jira call.
- Read `.agents/references/jira-conventions.reference.md` for labels and body
  rules.
- Read the site and cloud ID from the project profile or the user.

## Workflow

1. Authorize with `verify-jira-auth` when Jira is used. Stop when it fails.
1. Parse the issue key. Fetch the issue when the body is missing or stale. Read
   the summary, description, labels, status, and epic or component when
   relevant.
1. Ground the estimate in the repository.
   - Read the affected paths, import patterns, and configuration.
   - Prefer counts and concrete touch points over a vague claim.
   - Note explicit non-scope in the issue.
1. Assess readiness when the issue has a PRD or EDD label, or when the body
   clearly follows a core template.
   - Read `.agents/skills/create-prd/SKILL.md` and
     `.agents/skills/create-prd/prd-template.md`, or
     `.agents/skills/create-edd/SKILL.md` and
     `.agents/skills/create-edd/edd-template.md`.
   - Read `.agents/references/asd-ste100.reference.md` and
     `.agents/references/ears.reference.md`.
   - Compare the body with the template. Check for missing sections,
     placeholders, internal inconsistency, STE prose, and EARS requirements.
   - Build an internal backlog. Do not interview the user during triage.
   - Mark the issue ready only when the body is complete, the backlog is empty,
     and the open-questions section is absent, empty, or states that there are
     none.
   - Record a verdict: ready or not ready, with one reason.
1. Synthesize the effort.
   - Separate technical risk from delivery cost.
   - Give the assumptions and a range.
   - Avoid false precision.
   - Record the scan date when the metrics are time-sensitive.
1. Publish only when the user asks.
   - Edit the description or add a comment.
   - Merge labels. Never drop an unrelated label.
   - Add the readiness label only when the verdict is ready and the issue has a
     PRD or EDD.
   - Remove the readiness label when the verdict is not ready, the issue lacks
     a PRD or EDD, or readiness was not assessed.
   - Do not add the label for repository-only triage with no Jira write.

## Quality bar

- Cite verified paths and numbers from the repository. Flag uncertainty.
- Do not run git commands, migrations, or service operations unless the user
  explicitly asks.
- Do not imply that implementation is complete or that tests ran.

## Related

- `.agents/skills/verify-jira-auth/SKILL.md`
- `.agents/skills/create-jira-issue/SKILL.md`
- `.agents/skills/enrich-jira-issue/SKILL.md`
- `.agents/skills/create-prd/SKILL.md`
- `.agents/skills/create-edd/SKILL.md`
- `.agents/skills/review-jira-issue/SKILL.md`
- `.agents/references/jira-conventions.reference.md`
