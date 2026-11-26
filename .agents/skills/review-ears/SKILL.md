---
name: review-ears
description: Audits behavioral requirements for EARS syntax, testable obligations, and correct SHALL statements. Use when reviewing a specification or design document.
---

# Review EARS

Audit the behavioral requirements in a document. Report defects. Do not change
the intended behavior.

User-facing prompt reference:

- `.agents/prompts/review-ears.prompt.md`

## When to use

- The user asks for an EARS review or a requirements-syntax audit.
- A specification, design document, or draft contains behavioral `SHALL`
  statements.
- A review finds requirements that are vague, compound, or untestable.

For a conversational gap review, use `.agents/skills/conduct-interview/SKILL.md`
instead. This skill is a written audit.

## Inputs to inspect

- The target document or pasted text.
- `.agents/references/ears.reference.md`
- `.agents/references/asd-ste100.reference.md` for the prose inside each requirement.
- Related requirements, acceptance criteria, and design sections that give
  context.

## Workflow

1. Read the EARS standard and the target document.
1. Find every behavioral requirement, including acceptance criteria and
   definition-of-done items.
1. Check each requirement for one system, one `SHALL`, one testable obligation,
   and correct clause order.
1. Flag behavior that is written as prose instead of a requirement.
1. Propose a rewrite that preserves the intended behavior.
1. Ask before applying a rewrite when the intent is unclear.
1. Report findings by severity and state whether the document passes.

## Output format

```markdown
## Findings

- **High:** [Invalid or untestable requirement.] (`section`)
- **Medium:** [Ambiguous or compound requirement.] (`section`)
- **Low:** [Style or consistency issue.] (`section`)

## Proposed rewrites

- Before: [original sentence]
- After: [EARS sentence]

## Summary

[Pass or fail. State the remaining assumptions or limits.]
```

## Rules

- Preserve the author's intent. Do not invent behavior.
- Keep one obligation per requirement.
- Keep EARS keywords and `SHALL`.
- Write the non-keyword wording in STE.
- Do not force EARS on goals, non-goals, architecture narrative, or process
  checklists.
- If a requirement is discoverable only from code, read the code before you
  propose a rewrite.
