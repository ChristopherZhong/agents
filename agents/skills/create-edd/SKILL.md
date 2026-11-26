---
name: create-edd
description: Drafts or expands an engineering design document with STE prose, EARS contracts, and a verifiable definition of done. Use when creating or structuring an EDD.
---

# Create EDD

Use engineering-oriented language: current and target architecture, interfaces,
migration, risks, and a verifiable definition of done.

User-facing prompt reference:

- `.agents/prompts/create-edd.prompt.md`

## Documentation language

- Write prose in ASD-STE100. Read `.agents/references/asd-ste100.reference.md`.
- Write behavioral contracts, behavioral done criteria, and interface behavior in
  EARS. Read `.agents/references/ears.reference.md`.
- Keep the EARS keywords and `SHALL`. Write the rest of each requirement in STE
  style.
- Keep architecture narrative, file inventories, option comparisons, and process
  checklists in STE prose, not EARS.

## Discovery

Before drafting or materially expanding an EDD, read and follow
`.agents/skills/conduct-interview/SKILL.md`. Use its one-question-at-a-time
interview to clarify goals, constraints, interfaces, risks, rollout, testing,
and open decisions.

If open questions remain, stop drafting and resolve them through the interview.
Do not leave unresolved placeholders in the EDD unless the user asks for an
open-questions section.

## Review mode

When the user asks to find or resolve gaps, inconsistencies, or ambiguities in an
EDD:

1. Read and follow the specification review mode in
   `.agents/skills/conduct-interview/SKILL.md`.
1. Do not reply with a full list of every issue in one message.
1. Resolve one item at a time and wait for the user's answer.
1. After the items are resolved, offer to update the EDD.

A consolidated findings list is allowed only when the user asks for a full audit
or a written review.

## Template

Before drafting the body, read `.agents/skills/create-edd/edd-template.md`. Keep
the template as the source of truth for structure.

## Quality bar

- State the current design before the target design.
- Compare options when a decision is still open.
- Do not invent file paths, versions, or behavior.
- Make each done item verifiable.
- Keep process gates such as lint, test, and review as ordinary checkboxes.
- Keep the original request at the end of the document.

## Output

Report the document path or draft, the open questions, and the standards that
were applied.
