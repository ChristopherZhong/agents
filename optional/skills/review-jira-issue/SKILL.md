---
name: review-jira-issue
description: Reviews a Jira PRD or EDD for gaps, ambiguities, and inconsistencies through the core interview workflow, while a Jira specialist fetches data and applies agreed edits.
---

# Review Jira issue

Review a PRD or EDD that lives in Jira. This is planning work. It does not
implement code, run migrations, or start services.

This skill is part of an optional Jira bundle. Install the bundle only when the
repository uses Jira.

## Role split

This skill owns specification-review judgment. Jira API work belongs to
`jira-specialist`.

| Context | Judgment | Jira fetch and apply |
|---|---|---|
| Coordinator, parent, or main agent | Yes | No. Delegate to `jira-specialist`. |
| `jira-specialist` | No | Yes. Return data or apply the supplied edit. |
| User manually | Yes | Yes |
| Any other sub-agent | Yes, when asked | No |

When `jira-specialist` is asked to review an issue without finished review
decisions, it fetches and returns data only. It does not run an interview or
write a gap backlog.

## What this skill does not do

- Do not review an issue that has no PRD or EDD. Tell the user to run
  `.agents/skills/enrich-jira-issue/SKILL.md` first.
- Do not dump a full audit unless the user asks for one. Resolve one item at a
  time.
- Do not enrich or expand a thin issue. That is `enrich-jira-issue`.
- Do not call Jira directly. Do not run `verify-jira-auth`. Those steps run
  inside `jira-specialist`.

## Prerequisites

- A user-supplied issue key, or a key inferred from the branch.
- A pasted PRD or EDD body is acceptable. Use it and skip the fetch.
- Delegate every Jira call to `jira-specialist`.

## Workflow

1. Resolve the issue key.
   - When the user supplied a key, use it.
   - When the user pasted a full document, use that text and skip to step 3.
   - Otherwise infer a key only when the branch name clearly contains one.
     Otherwise ask the user and wait.
1. Delegate a fetch to `jira-specialist`. Ask for data only: summary,
   description, labels, issue type, status, and parent when relevant.
1. Confirm the issue with the user. Show the key, summary, type, status, and any
   PRD or EDD label. Ask whether this is the right issue. Stop when it is not.
1. Detect the document type.
   - A `PRD` label means PRD.
   - An `EDD` label means EDD.
   - Without a label, use the body when it clearly follows a core template.
   - When neither applies, stop and ask the user to enrich the issue first.
   - When both labels are present or the body is ambiguous, ask the user.
1. Load the core skill. For a PRD, read `.agents/skills/create-prd/SKILL.md`,
   `.agents/skills/create-prd/prd-template.md`,
   `.agents/references/asd-ste100.reference.md`, and
   `.agents/references/ears.reference.md`. For an EDD, read the EDD skill,
   template, and the same two references.
1. Ground the review in the repository when the issue concerns this repository.
   Verify the paths and versions that the issue cites.
1. Review through `.agents/skills/conduct-interview/SKILL.md` in specification
   review mode.
   - Build an internal backlog from the template, the EARS standard, the STE
     standard, and the repository facts.
   - Do not print the backlog.
   - Present one item per turn and wait for the answer.
1. Close out.
   - Summarize the resolved decisions.
   - Offer to apply the agreed changes to Jira.
   - Delegate the apply step to `jira-specialist`. Supply the exact description,
     summary, comment, and label changes. Merge the labels. Never drop an
     unrelated label.

## Quality bar

- The core skill owns the template semantics.
- `conduct-interview` owns the interview mechanics.
- This skill owns the document-type gate and the repository grounding.
- `jira-specialist` owns the fetch and the apply.
- Use verified paths and versions only.

## Related

- `.agents/skills/enrich-jira-issue/SKILL.md`
- `.agents/skills/conduct-interview/SKILL.md`
- `.agents/skills/create-prd/SKILL.md`
- `.agents/skills/create-edd/SKILL.md`
- `.agents/skills/triage-jira-issue/SKILL.md`
- `.agents/skills/review-ears/SKILL.md`
- `.agents/skills/review-ste100/SKILL.md`
- `.agents/references/jira-conventions.reference.md`
