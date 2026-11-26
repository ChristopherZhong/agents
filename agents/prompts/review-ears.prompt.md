# Review EARS Prompt

Audit the behavioral requirements in a document for EARS compliance.

Workflow reference:

- `.agents/skills/review-ears/SKILL.md`

Requirements:

- Read `.agents/references/ears.reference.md` first.
- Check every behavioral requirement and acceptance criterion.
- Report one system, one `SHALL`, and one testable obligation per requirement.
- Propose rewrites that preserve the intended behavior.
- Do not invent requirements or change scope.

Output format:

1. Findings by severity
1. Proposed rewrites
1. Pass or fail summary
