---
name: create-adr
description: Records a durable architecture decision when it is hard to reverse, surprising without context, and the result of a real trade-off. Use when a decision needs an ADR.
---

# Create ADR

Record a decision that a future reader cannot reconstruct from the code.

User-facing prompt reference:

- `.agents/prompts/create-adr.prompt.md`

## When to use

Create an ADR only when all three conditions are true:

- **Hard to reverse:** The cost of changing the decision later is meaningful.
- **Surprising without context:** A future reader will ask why the repository
  works this way.
- **Real trade-off:** Alternatives existed and the repository chose one for
  specific reasons.

If any condition is missing, do not create an ADR. Record the decision in the
nearest existing document instead.

## Inputs to inspect

- `docs/adr/` and its index, when present.
- `README.md` and `AGENTS.md` for repository conventions.
- Existing ADRs, to match naming and structure.
- The decision, the alternatives, and the consequences.

## Workflow

1. Confirm the three conditions. State which alternatives existed.
1. Inspect existing ADRs. Follow their file naming and section structure.
1. If no local format exists, propose the minimal format below and ask before
   writing.
1. Present the proposed record. Get approval before writing.
1. Write the record with an atomic file write.
1. Update the ADR index when one exists.
1. Link the record from affected documentation when the link helps discovery.

## File naming

Use the existing repository pattern. When none exists, use
`NNNN-short-kebab-title.md`.

- Use the next free four-digit number.
- Inspect the directory before choosing the number.
- Keep the title short and specific.
- Do not renumber existing records.

## Minimal format

```markdown
# NNNN — Short title

**Status:** Proposed | Accepted | Superseded · YYYY-MM-DD

## Context

Describe the forces, constraints, and why this decision exists.

## Decision

Describe the chosen approach.

## Consequences

Describe the positive, negative, and follow-up consequences.

## Alternatives rejected

- **Name the alternative:** State why it was not chosen.
```

## Output

Report the record path, the status, the alternatives, and any index or links
that changed.
