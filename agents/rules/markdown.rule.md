---
paths:
  - "*.md"
---

# Markdown Guidelines

- For numbered/ordered lists, always use `1.` for each item. Do not change `1.` to explicit numbers (e.g., `2.`, `3.`) to preserve Markdown auto-numbering. Explicit numbering breaks auto-numbering and requires manual renumbering when inserting items.
- For unordered lists, always use `-` (hyphen) instead of `*` (asterisk).
- For command-line examples, always use long-form options (e.g., `apt update --yes` instead of `apt update -y`).
- For script examples, always prefix commands with `$` to distinguish them from output.

## Documentation Writing Standards

### ASD-STE100 Simplified Technical English

- Apply ASD-STE100 to durable technical prose. Read
  `.agents/references/asd-ste100.reference.md` before writing or reviewing a technical
  document.
- Use the active voice, the present tense, short sentences, and one idea per
  sentence.

### EARS (Easy Approach to Requirements Syntax)

- Use EARS for behavioral requirements. Read `.agents/references/ears.reference.md` before
  writing or reviewing requirements.
- Every requirement names one system, contains one `SHALL`, and states one
  testable obligation.
