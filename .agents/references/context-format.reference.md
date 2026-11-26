# Context Format

Use this format for a new `.agents/context/<topic>.md` file. Replace the title
and section names with the topic.

```markdown
# Topic Context

**Purpose**: State what this note preserves for future work.

## Focused section

- **Term or pattern**: State the verified fact, decision, invariant, or
  convention.
```

## Rules

- Prefer an existing context file that matches the topic.
- Create a new file only when the durable information does not fit an existing
  file.
- Keep the note concise and specific to this repository.
- Record verified facts, decisions, invariants, and terms.
- Do not record temporary brainstorming.
- Do not record a rejected idea unless a future reader needs the reason.
- Do not record facts that are obvious from nearby code.
- Cite the source file, command, or decision when the fact is not obvious.
- Do not store secrets or personal data.
- Keep binding behavior in `.agents/rules/`, not in a context note.
