# EARS (Easy Approach to Requirements Syntax)

Canonical syntax for behavioral requirements in this repository. Source
patterns: [Easy Approach to Requirements Syntax](https://en.wikipedia.org/wiki/Easy_Approach_to_Requirements_Syntax)
(Mavin et al., RE'09).

Read this file before drafting or reviewing functional requirements, acceptance
criteria, or other system-`SHALL` statements. For an audit, use
`.agents/skills/review-ears/SKILL.md`.

Non-requirement technical prose uses `.agents/references/asd-ste100.reference.md`. In an
EARS sentence, keep the EARS keywords and `SHALL`. Write the rest of the sentence
in STE style.

## Ruleset

Each requirement is one sentence with:

- Zero or more preconditions (`WHILE`).
- Zero or one trigger (`WHEN`) or unwanted condition (`IF ... THEN`).
- Exactly one system name.
- One or more system responses.
- The modal `SHALL`.

Clauses appear in this order: `WHILE`, then `WHEN` or `IF/THEN`, then
`the <system> SHALL`.

Name the system concretely, such as `the report service` or
`the authentication service`. Do not use `the system` or `we` unless the actor
is genuinely unnamed.

## Patterns

| Pattern | Form | When to use |
|---|---|---|
| Ubiquitous | The \<system\> SHALL \<response\>. | Always active; no trigger. |
| Event-driven | WHEN \<trigger\>, the \<system\> SHALL \<response\>. | Response to a discrete event. |
| State-driven | WHILE \<precondition\>, the \<system\> SHALL \<response\>. | Active while a state holds. |
| Optional feature | WHERE \<feature is included\>, the \<system\> SHALL \<response\>. | Only for a product or variant that has the feature. |
| Unwanted behavior | IF \<unwanted condition\>, THEN the \<system\> SHALL \<response\>. | Faults, invalid input, failures, errors. |
| Complex | Combine keywords in one sentence. | Richer behavior; keep one obligation. |

Examples:

- Ubiquitous: The report service SHALL expose a health endpoint without
  authentication.
- Event-driven: WHEN a client sends a valid token, the authentication service
  SHALL identify the caller before the request reaches a route handler.
- State-driven: WHILE the queue is unavailable, the import worker SHALL reject
  new jobs with a retryable error.
- Optional: WHERE audit logging is enabled, the report service SHALL persist
  each export event.
- Unwanted: IF the request body fails validation, THEN the report service SHALL
  return a validation error with the failed fields.
- Complex: WHILE the service is shutting down, WHEN a new request arrives, the
  report service SHALL reject it with a retryable error.

## Numbering and lists

- Number each requirement so a review can cite it. Use `FR-1`, `AC-1`, or a
  numbered list.
- One behavior per requirement. Split compound sentences that contain `and
  then`.
- Prefer EARS for behavior. Use a table for attributes such as limits,
  retention periods, or service targets that are not a system response.

## What is not EARS

Do not force EARS for:

- Goals, non-goals, purpose, and problem statements.
- Architecture narrative, file inventories, and option comparisons.
- Pure metrics or constraints with no system response, such as a latency target.
- Process checklists such as lint, test, and review steps.

Rewrite fuzzy verbs such as `support`, `handle`, `integrate`, and `robust` into
a pattern above before publishing the requirement.

## Review checks

- Does the sentence contain exactly one `SHALL`?
- Does it name exactly one system?
- Does it contain exactly one testable obligation?
- Are `WHILE`, `WHEN`, and `IF/THEN` clauses in the correct order?
- Is the behavior concrete enough to test?
- Does the sentence avoid vague verbs and undefined terms?

For a full written audit, follow `.agents/skills/review-ears/SKILL.md`.
