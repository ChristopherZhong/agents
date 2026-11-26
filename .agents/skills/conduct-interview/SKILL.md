---
name: conduct-interview
description: Interviews the user persistently with targeted follow-up questions until reaching shared understanding of a topic, requirement, or decision.
---

# Relentless Interview

Use this skill when you need to extract clarity from a vague request, ambiguous requirement, or topic that requires deeper exploration. This skill drives interviews forward systematically until both parties share a common understanding.

## Use Cases

- Clarifying an unclear feature request before implementation
- Understanding the context behind a cryptic error or issue
- Exploring the scope and constraints of a new task
- Validating assumptions before making significant changes
- Gathering requirements when the user's intent is only partially clear
- Drilling into a decision to expose unstated constraints or concerns

## Question template

Use this structure for each turn:

```markdown
Current understanding: [one to three sentences]

Why this matters: [concrete dependency or risk]

Recommended answer: [choice grounded in repository evidence when possible]

Question: [one question only]
```

## Specification review mode

Use this mode when the user asks to find or resolve gaps, inconsistencies, or
ambiguities in a product requirements document (PRD), an engineering design
document (EDD), or another draft specification.

1. Read the whole document and build an internal backlog ordered by dependency.
   Do not print the backlog.
1. Read `.agents/references/ears.reference.md` and `.agents/references/asd-ste100.reference.md`.
   Compare the document with `.agents/skills/create-prd/prd-template.md` or
   `.agents/skills/create-edd/edd-template.md`.
1. Treat a missing or invalid EARS requirement as a review item.
1. Treat unclear or multi-topic prose as an STE review item when it blocks
   shared understanding.
1. Present only the current item. Never lead with a numbered list of every
   issue.
1. After each answer, mark the item resolved or deferred and continue with the
   next item.
1. When the backlog is empty, summarize the decisions and offer to update the
   document.

A consolidated report is allowed only when the user asks for a full audit.

## Workflow

### Phase 1: Initial Clarification

1. Identify the core ambiguity or area of unclear understanding.
1. Ask **one targeted, open-ended question** that directly addresses it.
1. Do NOT ask multiple questions at once—this dilutes focus and allows partial answers.

### Phase 2: Iterative Drilling

1. **Listen actively:** Parse the user's response for unstated assumptions, implicit constraints, and incomplete details.
1. **Ask follow-up questions:** For each response:
   - Ask **one question** at a time.
   - Ask it **immediately**—do not accumulate questions or wait for all information before asking more.
   - Make each question build directly on the previous response.
   - Go deeper into areas that reveal complexity, ambiguity, or unstated needs.
   - Avoid repeating information the user has already provided.
1. **Track assumptions:** Internally note assumptions that emerge and probe them when relevant.
1. **Persist:** Continue asking until you detect that both you and the user have consistent, shared understanding.

### Phase 3: Convergence & Confirmation

1. **Synthesize:** Summarize the shared understanding concisely in your own words.
1. **Confirm:** Ask the user: "Does this match your intent?"
1. **Resolve gaps:** If the user indicates misalignment, return to Phase 2.
1. **Close:** Once the user confirms alignment, document the shared understanding clearly (the user will likely want to reference it).

## Principles

- **One question per turn:** Rapid-fire questions feel like interrogation; one focused question per turn builds dialogue.
- **Go deep, not wide:** Don't ask "What about X, Y, and Z?" Ask about X; when answered, then ask about Y.
- **Follow the answer:** Let the user's responses guide the next question. Don't follow a predetermined list.
- **Surface hidden constraints:** Often the real issue is unstated constraints (budget, timeline, skill, dependencies). Probe for them.
- **No assumptions:** If you're uncertain, ask. Never infer when clarification is available.
- **Persistence with respect:** Keep asking until clarity emerges, but remain respectful and collaborative.

## Grounding

- Explore the repository before asking a factual question.
- Use `.agents/rules/`, `docs/`, `README.md`, tests, and configuration to answer
  what already exists.
- Ask the user only for intent, trade-offs, priorities, domain meaning, or
  choices that the repository cannot answer.
- Cite the files and symbols you verified.

## Recast agreed text

- When the user agrees on behavior, rewrite it as an EARS sentence per
  `.agents/references/ears.reference.md` before you treat the item as resolved. Write the
  non-keyword wording in STE.
- When the user agrees on background, architecture, or procedure text, rewrite
  it in ASD-STE100 per `.agents/references/asd-ste100.reference.md` before you treat the
  item as resolved.

## Durable decisions

- Update the nearest existing canonical file when a durable decision or term
  emerges. Prefer `.agents/rules/` for repository behavior and `docs/` for
  governance.
- Create a file only when the information does not fit an existing file.
- Offer an ADR only when all three conditions in
  `.agents/skills/create-adr/SKILL.md` are true. Otherwise, skip the ADR.
- Do not record temporary brainstorming or facts that are obvious from nearby
  code.

## Output Expectations

- The user should feel heard and understood, not interrogated.
- Both you and the user should articulate the same mental model of the problem, goal, or requirement.
- Ambiguities should convert into specific, actionable understanding.
- Unstated constraints and assumptions should surface and be acknowledged.
- The skill should conclude with a documented shared understanding that the user can reference.
