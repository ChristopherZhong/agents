---
name: onboard-contributor
description: Use when explaining this repository to a new contributor, producing an accurate overview of what exists today, how it is organized, and where to start.
---

# Repository Onboarding

Explain this repository to a new contributor using only what actually exists.

User-facing prompt reference:

- `.agents/prompts/repo-onboarding.prompt.md`

Use that prompt when you want a short reusable invocation for this workflow.
Treat this skill as the procedural source of truth and keep the prompt concise.

## Inputs to inspect

- `README.md`
- `AGENTS.md`
- `.agents/rules/`
- `.agents/skills/`, `.agents/prompts/`, `.agents/agents/`
- `.agents/config.yaml` — the upstream harness this repository syncs from
- The main source, manifest, or configuration directories
- Build, test, and task runner configuration
- `QUESTIONS.md` and `SUGGESTIONS.md`, when present

## Workflow

1. Inventory what exists: the files, directories, and tooling actually present
   in the repository today.
1. Describe the structure: the purpose of each major directory and the
   technologies in use.
1. Explain the workflows: how a change is made, reviewed, and delivered.
1. Describe the agent assets: how rules, skills, prompts, and agents relate,
   and how assets arrive from the upstream harness.
1. Separate implemented from planned: mark roadmap items clearly.
1. Surface gaps: note assumptions a newcomer must verify before changing
   anything.

## Output expectations

- An overview of what the repository is for.
- A clear inventory of what exists today.
- The structure, with each major directory explained.
- How to make a change safely, end to end.
- Roadmap items marked as planned, not as present.
- Assumptions and gaps called out.

## Grounding rules

- Reference only files and directories that exist.
- Do not invent tooling, workflows, or infrastructure.
- If something cannot be determined from the repository, say so. Add the
  question to `QUESTIONS.md` when that file exists.
- Keep the explanation short enough to read once and complete enough to prevent
  mistakes.

## Validation checklist

- [ ] Every file and directory mentioned exists.
- [ ] Every command shown is current.
- [ ] Planned work is marked as planned.
- [ ] No example references a removed file.
- [ ] Safety notes appear where operations are destructive.
- [ ] The explanation agrees with `README.md` and `AGENTS.md`.
