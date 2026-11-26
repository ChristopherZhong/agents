# ASD-STE100 (Simplified Technical English)

Canonical prose style for durable technical documentation in this repository.
Source: [ASD-STE100](https://www.asd-ste100.org/). The standard has two parts:

1. Writing rules (Part 1).
1. A controlled dictionary (Part 2).

This file is a repository guide for agents. It is not a copy of the standard. If
this guide and the official issue disagree, the official issue wins. Do not
paste large parts of the proprietary dictionary or rule text into the
repository.

Read this file before drafting or reviewing a technical document. For an audit,
use `.agents/skills/review-ste100/SKILL.md`.

## How STE works with EARS

| Content | Standard | Source of truth |
|---|---|---|
| Behavioral requirements and behavioral acceptance criteria | EARS first | `.agents/references/ears.reference.md` |
| All other technical prose | STE | This file |

Precedence for one EARS requirement:

1. Keep the EARS shape: `WHILE`, `WHEN`, `WHERE`, `IF ... THEN`, a named system,
   and `SHALL`.
1. Write the rest of the sentence in STE style.
1. Prefer a shorter EARS sentence. Split it into numbered requirements when you
   can.
1. Do not remove `SHALL` or EARS keywords to chase dictionary purity.

## Scope

In scope:

- Product requirements, design documents, and architecture decision records.
- Plans, runbooks, and operator procedures.
- Durable notes that explain architecture, operations, or decisions.
- Documentation written for humans to read later.

Out of scope:

- Source code and identifiers, including paths, package names, and API names.
- Commit messages and change titles.
- Ephemeral scratch notes unless the user asks for STE.
- Chat replies that are not documentation artifacts.

## Words and terms

- Prefer simple, consistent English.
- Use one word for one meaning in a document.
- Use technical nouns and technical verbs from the product domain when needed.
- Do not use slang, regional jargon, or metaphors as terms.
- Keep one technical noun for one thing in a document.
- Prefer American English spelling in new prose unless you quote an existing
  string.
- Define an abbreviation at first use. Use the abbreviation after that.

## Sentence and paragraph shape

- One topic per sentence.
- One instruction per procedural sentence.
- Maximum 25 words for a descriptive sentence (Part 1, rule 6.3).
- Maximum 20 words for a procedural or imperative sentence (Part 1, rule 5.1).
- Keep paragraphs short. Use a list for a sequence of steps.
- Put the condition before the action when the order affects the result.
- Avoid noun strings of more than three words.
- Avoid nested clauses when a second sentence is clearer.

## Verbs and voice

- Use active voice.
- Use present tense for current behavior.
- Use `SHALL` only for a binding requirement.
- Use `should` for a recommendation, and `can` for a capability.
- Do not use contractions.
- Do not use `will` for a requirement.
- Use one verb for one action. Do not rotate among synonyms.
- Avoid `-ing` forms when a direct verb is clearer.
- Avoid marketing words such as `seamless`, `robust`, `powerful`, and `easy`.

## Procedures

- Start each step with an imperative verb.
- Put one action in one step.
- State the condition before the step when the step is conditional.
- State the expected result when the result is not obvious.
- Put a warning before the action it protects.
- Use a note only for information that does not change the action.

## Ambiguity and consistency

- Replace `simple`, `fast`, `soon`, `nice`, and `support` with measurable
  behavior.
- Use the same term for the same object in the whole document.
- Do not use `etc.` or `and so on` when the list matters.
- Do not use a pronoun when the referent could be unclear.
- Keep the order of fields, labels, and steps stable.
- Use examples only when they clarify a rule that is hard to state.

## Review checks

- Is the sentence short enough?
- Is the voice active?
- Is the tense present?
- Is the term consistent with earlier text?
- Is the action or condition unambiguous?
- Does the sentence avoid contractions and vague words?
- Does the sentence state one idea?

For a full written audit, follow `.agents/skills/review-ste100/SKILL.md`. Cite
the relevant ASD-STE100 Part 1 rule when you report a defect.
