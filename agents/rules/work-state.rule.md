# Work state

- Use `.agents/sessions/` for active scratch notes, `.agents/context/` for
  durable notes, and `.agents/docs/` for plans.
- Use `.agents/skills/maintain-work-state/SKILL.md` when a task needs working
  memory.
- Read `.agents/references/work-state.reference.md` before creating or updating a
  work-state file.
- Do not commit session notes. Add `.agents/sessions/` to the repository ignore
  file.
- Promote verified durable facts to context and durable decisions to an ADR.
- Do not store secrets or unverified claims in any layer.
- Keep context concise. A context note is not a rule.
