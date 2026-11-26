# Review STE100 Prompt

Audit the technical prose in a document for ASD-STE100 compliance.

Workflow reference:

- `.agents/skills/review-ste100/SKILL.md`

Requirements:

- Read `.agents/references/asd-ste100.reference.md` first.
- Check words, terms, sentence length, voice, tense, and procedures.
- Keep EARS keywords and `SHALL` in behavioral requirements.
- Propose rewrites that preserve the meaning.
- Do not remove requirements, conditions, or warnings.

Output format:

1. Findings by severity
1. Proposed rewrites
1. Pass or fail summary
