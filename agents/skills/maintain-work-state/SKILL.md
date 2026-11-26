---
name: maintain-work-state
description: Maintains session notes, durable context notes, and plans across a task. Use when starting, updating, or closing non-trivial work, or when a task needs working memory.
---

# Maintain Work State

Keep working memory in the correct layer. Promote durable content. Discard
scratch content.

User-facing prompt reference:

- `.agents/prompts/maintain-work-state.prompt.md`

## When to use

- Starting a non-trivial task that needs scratch state.
- Updating a plan when scope, risks, or validation change.
- Promoting a verified fact to durable context.
- Closing a task and deciding what to keep.

## Inputs to inspect

- `.agents/references/work-state.reference.md`
- `.agents/references/context-format.reference.md`
- `.agents/sessions/`, when it exists.
- `.agents/context/`, when it exists.
- `.agents/docs/`, when it exists.
- The task state, decisions, and open questions.

## Workflow

1. Choose the layer. Use a session note for active scratch, context for durable
   facts, and a plan for non-trivial work.
1. Create a file only when the task needs it. Prefer an existing file.
1. Use the naming convention from `.agents/references/work-state.reference.md`.
1. Record verified facts. Mark an uncertain item as open.
1. Update the note or plan when the state changes.
1. Promote a durable fact to context and a durable decision to an ADR.
1. Close the task by removing or ignoring the session note.

## Rules

- Do not store secrets, credentials, tokens, or personal data.
- Do not copy unverified claims into durable context.
- Do not turn a context note into a rule. Put binding behavior in
  `.agents/rules/`.
- Do not commit session notes.
- Do not create all three layers for a small task.
- Ask when the correct layer or the durable content is unclear.

## Output

Report the paths created or updated, the facts promoted, the decisions that need
an ADR, and any open questions.
