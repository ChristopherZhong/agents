# Maintain Work State Prompt

Maintain the session notes, durable context, and plans for this task.

Workflow reference:

- `.agents/skills/maintain-work-state/SKILL.md`

Requirements:

- Read `.agents/references/work-state.reference.md` and
  `.agents/references/context-format.reference.md` first.
- Choose the correct layer: session, context, or plan.
- Create a file only when the task needs it. Prefer an existing file.
- Record verified facts. Mark open questions as open.
- Promote durable facts to context and durable decisions to an ADR.
- Do not store secrets. Do not commit session notes.

Output format:

1. Paths created or updated
1. Facts promoted to context
1. Decisions that need an ADR
1. Open questions
