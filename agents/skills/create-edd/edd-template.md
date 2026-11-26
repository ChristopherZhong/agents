# Engineering Design Document

Use a short engineering title. Do not add a document-type prefix.

Write section prose in ASD-STE100 per `.agents/references/asd-ste100.reference.md`. Write
behavioral contracts and behavioral done criteria in EARS per
`.agents/references/ears.reference.md`.

Adapt the sections to the topic. Omit a section only when it is clearly not
applicable.

| Field | Value |
|---|---|
| Scope | Name the repository, service, or component. |
| Doc type | EDD |
| Related items | List the links or identifiers. |

## Background

State the motivation, the current problem, and the links to related documents.

## Current architecture

Describe the components, file paths, contracts, data flow, and constraints that
exist today.

## Target architecture

Describe the design. When a decision is open, present Option A and Option B and
state a recommendation.

## Implementation plan

List the ordered steps from investigation to rollout and cleanup.

## Testing strategy

Cover unit, integration, contract, and end-to-end tests as relevant.

## Observability and operations

Cover probes, metrics, logs, alerts, and runbooks when relevant.

## Risks and mitigations

| Risk | Impact | Mitigation |
|---|---|---|
| Describe the risk. | Describe the impact. | Describe the mitigation. |

## Definition of done

Write behavioral items as EARS sentences. Keep process gates as ordinary
checkboxes.

- [ ] Write a behavioral done item in EARS.
- [ ] Lint passes.
- [ ] Tests pass.
- [ ] Build passes.

## Open questions

Number the decisions that are still open. Remove this section when no question
remains.

---

_Original request (preserved):_ Quote the prior request or summary.
