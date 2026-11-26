---
name: review-skill
description: Reviews a skill for naming, scope, workflow, safety, and token load before it is kept. Use when creating, changing, or reviewing a skill.
---

# Review Skill

Review a skill as a future agent would use it. Prefer concrete defects over style
preferences.

User-facing prompt reference:

- `.agents/prompts/review-skill.prompt.md`

## When to run

- After creating or materially changing any skill under `.agents/skills/`.
- When the user asks to review, validate, or optimize a skill.
- For each changed skill directory when one task changes more than one skill.

Run this review before reporting that skill work is complete.

## Inputs to inspect

- The skill directory and its `SKILL.md`.
- Every support file that `SKILL.md` references.
- `.agents/rules/naming-conventions.rule.md`
- `.agents/rules/markdown.rule.md`
- `.agents/rules/agent-behavior.rule.md`
- Related prompts and agents when the skill is part of a workflow.

## Review checklist

- **Naming:** The directory uses `<verb>-<noun>`. The frontmatter `name`
  matches the directory.
- **Discovery:** The `description` is specific, third person, and contains the
  phrases that should trigger the skill.
- **Scope:** The skill states what it does, what it does not do, and when to ask
  for clarification.
- **Workflow:** Steps are ordered, actionable, and complete enough for a future
  agent to follow without guessing.
- **Consistency:** Terms, paths, command names, and output labels are stable.
- **Gaps:** Required inputs, prerequisites, permissions, validation steps, and
  expected outputs are present.
- **Ambiguity:** Instructions avoid vague phrases when a decision rule is
  possible.
- **Safety:** The skill respects repository rules for git, data, services,
  secrets, and destructive operations.
- **Maintainability:** `SKILL.md` is short enough to load directly. Move bulky
  examples or references into one-level support files.
- **Token efficiency:** Remove repetition and filler without removing required
  behavior.

## Token efficiency

Shorten the skill where possible. Do not remove:

- Required steps, prerequisites, or validation gates.
- Safety rules.
- Decision rules that prevent ambiguity or wrong behavior.
- Trigger phrases that discovery needs.

Safe reductions include duplicate rules, long prose that becomes a table,
overlapping sections, repeated restatements, and large examples that can move
to a support file.

Stop shortening when a future agent would need to guess intent, skip a gate, or
lose a non-obvious constraint.

## Workflow

1. Read the changed skill directory and every file it references.
1. Review the skill against the checklist.
1. Apply High and Medium fixes. Apply Low fixes when they are quick.
1. Re-check the result when the fixes are material.
1. Report what changed and whether the skill is ready.

## Output format

Use this structure when the user asks for a written review:

```markdown
## Findings

- **High:** [Issue and why it matters.] (`path`)
- **Medium:** [Issue and why it matters.] (`path`)
- **Low:** [Issue and why it matters.] (`path`)

## Open Questions

- [Question that blocks confidence, if any.]

## Summary

[One short paragraph on whether the skill is ready, needs edits, or needs redesign.]
```

If there are no issues, say so. State any review limit or assumption.
