# api-gateway `.agents` comparison

**Date:** 2026-11-25

**Scope:** Compare the `.agents/` tree in the `api-gateway` repository with this
repository's payload and installed copy. Identify features that could move into
the payload, features that need adaptation, and features that conflict with an
accepted decision.

## Method

- Read both `AGENTS.md` files, every rule in this repository, and every skill
  and agent frontmatter in both trees.
- Read the api-gateway reference documents, context notes, skill bodies, agent
  bodies, and the `.harness/` runner documentation.
- Read this repository's accepted ADRs, non-goals, support matrix, and sync
  cases.
- Ran `python3 .agents/scripts/validate.py` on this repository. Result:
  `payload mode: 0 error(s), 0 warning(s)`.
- The analysis below was produced before implementation. Waves 1-4 were then
  implemented and self-synced. See `Implementation status`.

## Short answer at analysis time

The two trees solve different problems.

- This repository is a portable, generic payload. It ships rules, skills,
  prompts, agents, and one validator. It has strong distribution mechanics and
  weak authoring depth.
- api-gateway is a project-specific operating system. It has deep documentation
  standards, spec-authoring workflows, specialist roles, and an autonomous flow
  runner. It has no distribution mechanics.

The best imports are the documentation standards, the skill-review gate, and
the spec-authoring workflows. The compatibility symlinks and the flow runner
conflict with accepted decisions. The Jira, GitLab, NestJS, and Prisma skills
are consumer-specific and must not enter the core payload as written. The Jira
and GitLab workflows now ship as opt-in bundles under `optional/`.

## Snapshot at analysis time

| Measure | This repository | api-gateway |
|---|---|---|
| Canonical rules | `AGENTS.md` plus 5 rule files | `AGENTS.md` (12 KB) |
| Skills | 11 | 23 |
| Agent definitions | 5 | 12 |
| Prompts | 9 | 0 |
| Rules | 5 | 0 |
| Context notes | 0 | 4 |
| Reference standards | 0 | 5 |
| Harness runner | none | 37 files under `.harness/` |
| Compatibility links | none | `.claude`, `.cursor`, `CLAUDE.md` |
| Validator | `.agents/scripts/validate.py` | none under `.agents/` |
| Distribution model | Commit-pinned three-way sync | None |
| Genericity enforcement | Validator denylist and review | None |

## Structural differences

| Dimension | This repository | api-gateway | Consequence |
|---|---|---|---|
| Product boundary | `agents/` is the product. `.agents/` is a self-synced copy. | `.agents/` is the product. No distributable copy. | A feature can move here only when it is generic. |
| Rule location | `.agents/rules/`, one topic per file. `AGENTS.md` is a short router. | Most rules live in `AGENTS.md`. No rule directory. | api-gateway rules are prose-heavy and consumer-specific. |
| Prompt layer | First-class `.agents/prompts/` invocations. | No prompt directory. Skills and `AGENTS.md` carry triggers. | api-gateway has no reusable user-facing prompt pattern. |
| Agent schema | YAML frontmatter with `name`, `description`, `scope`, `inputs`, `outputs`. File suffix `.agent.md`. | YAML frontmatter with `name`, `description`, `tools`. File suffix `.md`. | api-gateway agents fail this repository's naming and frontmatter checks as written. |
| Standards depth | Short standards inside `markdown.rule.md`. | Dedicated `reference/ears.md`, `reference/asd-ste100.md`, and review workflows. | This repository has a stub; api-gateway has the full operating model. |
| Durable knowledge | None. | `context/` for durable notes and `reference/` for standards. | api-gateway separates always-read rules from on-demand reference. |
| Work state | None. | `sessions/` for scratch (gitignored) and `docs/` for plans. | api-gateway has an explicit plan and session lifecycle. |
| Harness support | Neutral. `AGENTS.md` only. | Symlinks and a Cursor adapter. | api-gateway is optimized for Claude Code and Cursor. |
| Validation | Layout, naming, references, secrets, config, self-sync, genericity. | None in `.agents/`. Quality gates are project commands. | This repository can enforce imports mechanically. |
| Automation | No execution. Sync reads and writes files only. | Python flow runner executes agent sessions. | The runner conflicts with two non-goals. |

## Feature assessment

Fit labels:

- **Direct** — generic and compatible with current decisions.
- **Adapt** — useful pattern, but the text or structure must be rewritten.
- **Decision** — conflicts with an accepted ADR or a non-goal.
- **Consumer-only** — depends on the api-gateway stack or platforms.
- **Optional bundle** — reusable after de-branding, but kept out of the core
  payload under `optional/`.

| Feature | api-gateway implementation | Fit | Assessment |
|---|---|---|---|
| Skill quality gate | `review-skill` skill, mandatory after skill edits | Direct | Fills a real gap. Layout validation does not judge quality. |
| Interview workflow | `grill-me` skill with one-question turns and a fixed template | Adapt | `conduct-interview` already covers the core. Merge the missing parts; do not add a duplicate. |
| PRD authoring | `create-prd` skill and `prd-template.md` | Adapt | Useful generic workflow. Strip Jira conventions and explicit numbering. |
| EDD authoring | `create-edd` skill and `edd-template.md` | Adapt | Useful generic workflow. Strip stack and Jira specifics. |
| EARS standard | `reference/ears.md`, `review-ears`, `ears-specialist` | Adapt | This repository mentions EARS in one rule but ships no canonical syntax or audit workflow. |
| ASD-STE100 standard | `reference/asd-ste100.md`, `review-ste100`, `ste100-specialist` | Adapt | Same gap as EARS. Needs a generic reference file, not a project guide. |
| ADR authoring | Trigger criteria and format inside `grill-me` support files | Direct | This repository has ADRs but no workflow that creates them. |
| Context-note format | `context-format.md` and four context notes | Adopt | The format is generic. The notes are consumer-owned and must not ship. |
| Plan and session layers | `.agents/docs/` plans and `.agents/sessions/` scratch | Adopt | Ships a convention, an ignore requirement, and ADR 0014. The payload does not ship the directories. |
| Compatibility symlinks | `.claude` to `.agents`, `.cursor` to adapter, `CLAUDE.md` to `AGENTS.md` | Reject | ADR 0006 and `docs/non-goals.md` reject harness-specific files. Confirmed by decision. |
| Cursor adapter rule | `.agents/adapters/cursor/rules/agents.mdc` | Reject | Same conflict. Also vendor-specific. Confirmed by decision. |
| Specialist agent set | Orchestrator, architecture, implementation, health, docs keeper | Adapt | The role pattern is reusable. The bodies are api-gateway-specific. |
| Platform I/O specialists | `jira-specialist`, `gitlab-specialist` | Optional bundle | The role is reusable after de-branding. The first bundles are Jira and GitLab. |
| Judgment versus I/O split | Review skills judge; specialists fetch and post | Optional bundle | Valuable generic delegation rule. Shipped in the Jira and GitLab bundles. |
| Worktree workflow | `create-git-worktree` plus protected-branch rule | Adopt | Generic git skill. The consumer provides `.env` and dependency setup. |
| Autonomous flow runner | `.harness/agent-flows/` with 10 categories | Decision | Conflicts with "Not an agent runtime", "No automatic execution", and "No CI workflow shipped". |
| Jira and GitLab skills | 11 create, review, verify, and triage skills | Optional bundle | Jira and GitLab bundles ship under `optional/` as Group A. Dependency-update triage (`snyk-renovate`) is Group C and kept out. |
| Stack skills | `nestjs-module`, `prisma-repository`, startup and e2e checks | Deferred bundle | Names a technology stack. Allowed under `optional/`, not in the core payload. |
| Validation evidence rule | `reference/validation-standards.md` | Adapt | The principle is generic. The commands are consumer-specific. |
| PLAN and EXECUTE modes | Explicit mode contract in `AGENTS.md` | Open | This repository asks before acting but defines no mode boundary. Generic orchestration is under consideration. |
| Hard prohibitions | Data, services, git, Jira, GitLab, worktrees | Adapt | Generic safety rules exist. Service and platform rules are consumer-specific. |
| Templates as support files | `prd-template.md`, `edd-template.md`, `adr-format.md` | Direct | The one-level support-file pattern already fits the payload. |
| Frontmatter `tools` field | Agent tool allowlists | Consumer-only | This repository is tool-agnostic. Do not add a vendor field, even under `optional/`. |
| Branch policy file | `.harness/branching.yaml` | Consumer-only | Runner configuration. |

## What api-gateway exposes as gaps here

These gaps were present before Waves 1-4.

1. No quality gate runs after a skill is created or edited. `validate-ai-assets`
   checks layout. `review-prompts` checks prompts. No asset checks skill
   quality. Resolved by `review-skill`.
1. EARS and ASD-STE100 appear as a short subsection in `markdown.rule.md`. There
   is no canonical syntax file, no example set, and no audit workflow. Resolved
   by the reference standards and review workflows.
1. No generic workflow creates a PRD, EDD, or ADR. Resolved by the authoring
   skills.
1. No durable context convention exists. Every fact either becomes a rule, a
   prompt, or documentation. Resolved by the work-state layers.
1. No generic branch or worktree safety workflow exists. `git-workflow.rule.md`
   covers commits only. Resolved by `create-worktree`.
1. No completion standard requires command evidence. `agent-behavior.rule.md`
   asks for verification, but does not define evidence.
1. No orchestration pattern connects multiple agent roles to one task. Under
   consideration.

## What this repository has that api-gateway lacks

- Commit-pinned, three-way sync with explicit collision handling.
- A validator that enforces naming, frontmatter, references, secrets, and
  genericity.
- A self-sync invariant between payload and installed copy.
- A rules directory and a prompts directory.
- Generic agent frontmatter with `scope`, `inputs`, and `outputs`.
- ADRs, non-goals, a support matrix, sync-case evidence, and a changelog.
- Tested sync cases and documented gaps.
- Neutrality across agent harnesses.

These differences are the reason to import selectively. The payload's value is
portability. A feature that names a platform, a stack, or a harness reduces that
value.

## Import constraints

Any adopted feature must pass these checks.

| Constraint | Source | Effect on api-gateway assets |
|---|---|---|
| Agent suffix is `.agent.md` | Validator `check_naming` | Rename every imported agent file. |
| Agent frontmatter needs `name`, `description`, `scope`, `inputs`, `outputs` | Validator `check_frontmatter` | Add the missing keys and drop `tools`. |
| Skill directory must be `<verb>-<noun>` | Validator `check_naming` | `grill-me` fails. Reuse `conduct-interview`. |
| Ordered lists use `1.` for every item | `markdown.rule.md` and validator | Convert numbered templates such as `prd-template.md`. |
| References must resolve | Validator `check_references` | Rewrite `.agents/agents/*.md` references to `.agent.md`. |
| Payload text must be generic | `CONTRIBUTING.md`, ADR 0005, validator `check_genericity` | Remove Jira, GitLab, NestJS, Prisma, and repository names from `agents/`. Optional bundles are exempt from genericity, but not from consumer names. |
| No placeholders | ADR 0005 | Templates cannot contain project-name tokens. |
| `AGENTS.md` only | ADR 0006 and non-goals | Reject symlinks, adapters, and `CLAUDE.md`. |
| No execution of fetched content | ADR 0007 and non-goals | Reject the flow runner and any post-sync hook. |
| One shipped validator | ADR 0012 | Do not ship per-skill scripts. |
| No declared state | `CONTRIBUTING.md` | Do not add `mode` or status fields to frontmatter. |

Two structural notes:

- The payload mapping is generic (`agents/<path>` maps to `.agents/<path>`), so
  a new `agents/references/` directory needs no sync change.
- The validator does not reject extra directories. It only warns when the six
  expected directories are missing. Adding `references/` therefore needs a
  validator and documentation decision, not a sync change.

## Recommendations

### Wave 1 — adopt directly

1. Add `review-skill` as a payload skill, with a prompt and a thin
   `skill-reviewer.agent.md`.
1. Add `create-adr` as a payload skill that uses the ADR trigger criteria and
   format from `grill-me` support files.

Rationale: both fill gaps, both are generic, and neither needs a new directory
or a new convention.

### Wave 2 — adopt standards

1. Add `agents/references/ears.reference.md` and
   `agents/references/asd-ste100.reference.md` as
   generic standards.
1. Remove the duplicated summaries from `markdown.rule.md` and point to the
   reference files.
1. Add `review-ears` and `review-ste100` skills, plus
   `requirements-reviewer.agent.md` and `prose-reviewer.agent.md`.
1. Add prompts for both reviews.

Rationale: the reference layer keeps always-read rules short and loads detail
on demand. This is api-gateway's strongest structural idea.

### Wave 3 — adopt authoring workflows

1. Add `create-prd` and `create-edd` with generic templates.
1. Merge the valuable parts of `grill-me` into `conduct-interview`:
   - PRD and EDD review mode.
   - EARS recast of agreed behavior.
   - STE recast of agreed prose.
   - ADR trigger criteria.
   - Durable-note decision rules.
1. Do not add `grill-me` as a second interview skill. Two skills would duplicate
   one workflow and violate the `align-assets` convention.

Rationale: authoring is the missing half of the standards work. Merging avoids
the naming and duplication problems.

### Wave 4 — adopt in part

1. Context, plan, and session directories. Adopted as a convention, not as
   shipped directories. `references/work-state.reference.md` and
   `references/context-format.reference.md` define the layers. ADR 0014
   records the decision. The payload ships the convention and the ignore
   requirement.
1. Worktree workflow. Adopted as the generic `create-worktree` skill. The
   consumer provides the setup commands. The skill never removes a worktree,
   deletes a branch, or copies secrets.
1. Compatibility adapters. Excluded by decision. ADR 0006 and the non-goal
   apply. Tool neutrality is binding.
1. Orchestration and modes. Under consideration. A generic orchestrator is not
   implemented. The payload keeps its ask-before-act behavior.

### Wave 5 — optional bundles

1. Add `optional/` as a root sibling of `agents/`. It mirrors the payload
   layout and is not synced. ADR 0015 records the decision.
1. Add the Jira bundle: `jira-specialist`, `verify-jira-auth`,
   `create-jira-issue`, `enrich-jira-issue`, `review-jira-issue`,
   `triage-jira-issue`, a conventions reference, and prompts. Remove the
   api-gateway site, project key, epics, and workspace assumptions.
1. Add the GitLab bundle: `gitlab-specialist`, `verify-gitlab-auth`,
   `create-merge-request`, `update-merge-request`, `review-merge-request`, a
   conventions reference, a merge-request template, and prompts. Remove the
   api-gateway project path, default branch, and stack assumptions.
1. Defer dependency-update triage, stack bundles, and orchestration.

Rationale: a consumer that uses Jira or GitLab gets the workflow without
forcing a platform on every other consumer.

### Reject as written

1. The `.harness/` flow runner. It conflicts with the runtime, execution, and CI
   non-goals.
1. Jira, GitLab, NestJS, Prisma, startup, and e2e assets as core payload files.
   They are consumer specific. Jira and GitLab ship as de-branded optional
   bundles.
1. api-gateway's domain agent bodies and hard prohibitions. They describe one
   service lifecycle and one platform pair.
1. The `tools` frontmatter field. It couples assets to one harness, including
   under `optional/`.

## Implementation status

Waves 1-3 are implemented in full. Wave 4 is implemented in part. Wave 5 is
implemented for Jira and GitLab. All implemented payload assets are self-synced
to `.agents/`. Optional bundles are not self-synced.

- Wave 1: `review-skill` and `create-adr`, with prompts and thin agents.
- Wave 2: `references/ears.reference.md`,
  `references/asd-ste100.reference.md`, `review-ears`, `review-ste100`,
  reviewer agents, and prompts.
- Wave 3: `create-prd`, `create-edd`, templates, prompts, and `spec-author`.
  `conduct-interview` now covers specification review, grounding, agreed-text
  recast, and durable decisions.
- Wave 4: `references/work-state.reference.md`,
  `references/context-format.reference.md`, the `work-state` rule,
  `maintain-work-state`, `create-worktree`, prompts, and agents. ADR 0014
  records the work-state layers.
- Wave 5: Jira and GitLab bundles under `optional/`. ADR 0015 records the
  boundary. Dependency-update triage, stack bundles, and orchestration are
  deferred.
- Excluded: compatibility adapters. Under consideration: generic orchestration.

The validator now expects a `references/` directory in both payload and
installed mode. It also exempts the on-demand context, docs, and sessions
directories from the reference-existence check. It scans `optional/` for
layout, naming, frontmatter, and references, but skips genericity and
self-sync.

## Resolved decisions

- Compatibility adapters stay out. Tool neutrality is binding. ADR 0006 and
  `docs/non-goals.md` apply.
- Generic orchestration is under consideration. No orchestrator, mode contract,
  or flow runner is implemented.
- Keep `references/` for on-demand standards and `rules/` for short, always-read
  conventions. A long standard goes to `references/`. A binding convention gets
  a short rule that points to the reference file.
- Platform and stack assets stay out of `agents/`. Jira and GitLab ship as
  de-branded bundles under `optional/` as Group A. ADR 0015 records the
  boundary. Stack bundles and orchestration remain deferred.
- Dependency-update triage (`snyk-renovate`) is Group C. Do not add it now. It
  names a GitLab and npm workflow, and the core GitLab bundle stays neutral.

## Open decisions

1. Generic orchestration: should the payload define a generic orchestration
   pattern, and if so, which role boundaries belong in it?
1. Stack bundles: should the optional directory ship NestJS and Prisma bundles,
   or should each stack stay consumer-owned?
