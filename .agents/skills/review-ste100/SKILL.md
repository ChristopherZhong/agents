---
name: review-ste100
description: Audits technical prose for ASD-STE100 clarity, short sentences, active voice, and consistent terms. Use when reviewing a document for Simplified Technical English.
---

# Review STE100

Audit technical prose in a document. Report defects. Do not weaken EARS
requirements to satisfy a style rule.

User-facing prompt reference:

- `.agents/prompts/review-ste100.prompt.md`

## When to use

- The user asks for an STE, ASD-STE100, or Simplified Technical English review.
- A specification, design document, plan, runbook, or durable note needs a
  prose review.
- A review finds long sentences, passive voice, inconsistent terms, or vague
  wording.

For a conversational gap review, use `.agents/skills/conduct-interview/SKILL.md`
instead. This skill is a written audit.

## Inputs to inspect

- The target document or pasted text.
- `.agents/references/asd-ste100.reference.md`
- `.agents/references/ears.reference.md` for behavioral requirements.
- Related documents that establish terms and conventions.

## Workflow

1. Read the STE standard and the target document.
1. Check words, terms, sentence length, voice, tense, and paragraph shape.
1. Check procedures for one action per step and clear conditions.
1. Check behavioral requirements for valid EARS before you review their prose.
1. Propose a rewrite that preserves the meaning.
1. Ask before applying a rewrite when the intent is unclear.
1. Report findings by severity and state whether the document passes.

## Output format

```markdown
## Findings

- **High:** [Meaning or safety defect.] (`section`)
- **Medium:** [Clarity or consistency defect.] (`section`)
- **Low:** [Style issue.] (`section`)

## Proposed rewrites

- Before: [original sentence]
- After: [STE sentence]

## Summary

[Pass or fail. State the remaining assumptions or limits.]
```

## Rules

- Keep the meaning. Do not remove a requirement, condition, or warning.
- Keep EARS keywords and `SHALL` in behavioral requirements.
- Prefer the active voice and present tense.
- Prefer one idea per sentence.
- Cite the relevant ASD-STE100 Part 1 rule when you report a defect.
- Do not apply STE to code, identifiers, paths, or commit messages.
- Treat a long EARS sentence as a Low finding. Do not remove `SHALL` to shorten
  it.
