---
name: create-prd
description: Drafts or expands a product requirements document with STE prose and EARS behavioral requirements. Use when creating or structuring a PRD.
---

# Create PRD

Use product-oriented language: problems, goals, scope, user or operator value,
and measurable acceptance.

User-facing prompt reference:

- `.agents/prompts/create-prd.prompt.md`

## Documentation language

- Write prose in ASD-STE100. Read `.agents/references/asd-ste100.reference.md`.
- Write functional requirements and acceptance criteria in EARS. Read
  `.agents/references/ears.reference.md`.
- Keep the EARS keywords and `SHALL`. Write the rest of each requirement in STE
  style.
- Keep a numeric non-functional requirement as a number or a short STE sentence
  when it has no system response.

## Discovery

Before drafting or materially expanding a PRD, read and follow
`.agents/skills/conduct-interview/SKILL.md`. Use its one-question-at-a-time
interview to clarify the problem, goals, users, scope, measurable acceptance,
dependencies, rollout, and open decisions.

If open questions remain, stop drafting and resolve them through the interview.
Do not leave unresolved placeholders in the PRD unless the user asks for an
open-questions section.

## Review mode

When the user asks to find or resolve gaps, inconsistencies, or ambiguities in a
PRD:

1. Read and follow the specification review mode in
   `.agents/skills/conduct-interview/SKILL.md`.
1. Do not reply with a full list of every issue in one message.
1. Resolve one item at a time and wait for the user's answer.
1. After the items are resolved, offer to update the PRD.

A consolidated findings list is allowed only when the user asks for a full audit
or a written review.

## Template

Before drafting the body, read `.agents/skills/create-prd/prd-template.md`. Keep
the template as the source of truth for structure.

## Quality bar

- Prefer concrete, falsifiable statements over vague intent.
- Do not invent file paths, versions, or behavior.
- Keep goals and non-goals separate.
- Put one testable obligation in each requirement.
- Keep the original request at the end of the document.

## Output

Report the document path or draft, the open questions, and the standards that
were applied.
