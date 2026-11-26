# Work State

Use three layers. Keep each layer for one purpose.

| Layer | Path | Lifecycle | Tracked |
|---|---|---|---|
| Session | `.agents/sessions/` | Active task only | No; ignored by git |
| Context | `.agents/context/` | Durable facts and decisions | Yes |
| Plans | `.agents/docs/` | Plans for non-trivial work | Yes when useful |

## Session notes

- Create a session note only when a task needs scratch state.
- Name the file `session-YYYYMMDD-HHMMSS.md`.
- Record the goal, current state, decisions, open questions, and next step.
- Update the note during the task. Compact or rewrite it when it becomes large.
- Do not commit session notes. Add `.agents/sessions/` to the repository ignore
  file.
- Do not put secrets, credentials, tokens, or personal data in a session note.

## Durable context

- Use context notes for verified facts, invariants, decisions, and terms that a
  future task needs.
- Name the file `<topic>.md`.
- Prefer an existing file over a new one.
- Read `.agents/references/context-format.reference.md` before creating a file.
- Keep notes short. Remove facts that are obvious from nearby code.
- Do not record temporary brainstorming or rejected ideas that have no future
  relevance.
- A context note is not a rule. Put binding behavior in `.agents/rules/`.
- Cite the source of a fact when the source is not obvious.

## Plans

- Use a plan for non-trivial work that needs approval or multiple steps.
- Name the file `plan-YYYYMMDD-HHMMSS.md` under `.agents/docs/`.
- Include the goal, scope, steps, validation, risks, and open decisions.
- Update the plan when the scope changes.
- Do not treat a plan as a contract. Put a durable decision in an ADR.
- Commit a plan only when the repository wants the plan in history.

## Promotion

1. Start in a session note while the task is active.
1. Promote a verified, durable fact to `.agents/context/`.
1. Promote a decision that meets the three ADR conditions to `docs/adr/` through
   `.agents/skills/create-adr/SKILL.md`.
1. Keep a plan in `.agents/docs/` when the work needs review or history.
1. Remove or ignore the session note when the task ends.

## Boundaries

- Do not store secrets in any layer.
- Do not copy unverified claims into context.
- Do not create all three layers for a small task.
- Do not replace `.agents/rules/` or `.agents/references/` with context notes.
