# Changelog

Notable changes to the payload. Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

This project does not use semantic versions. Consumers pin a commit; see
`docs/adr/0004-commit-pinned-sync.md`.

## Unreleased

### Added

- Initial payload: 5 rules, 11 skills, 9 prompts, 5 agents, and
  `scripts/validate.py`.
- Documentation standards: `references/ears.reference.md`,
  `references/asd-ste100.reference.md`, `review-ears`, `review-ste100`,
  reviewer agents, and prompts.
- Specification authoring: `create-prd`, `create-edd`, and `create-adr` skills
  with templates, prompts, and agents.
- `review-skill` skill, prompt, and `skill-reviewer` agent.
- Work-state convention: `work-state` rule,
  `references/work-state.reference.md`,
  `references/context-format.reference.md`, `maintain-work-state` skill,
  prompt, and `work-state-maintainer` agent.
- Generic worktree workflow: `create-worktree` skill, prompt, and
  `worktree-creator` agent.
- `references/` as a payload directory, with a validator structure check.
- `sync-agents` skill and `agents-maintainer` agent.
- Governance: `CONTRIBUTING.md`, `SECURITY.md`, `docs/adr/`, support matrix,
  and non-goals.
- ADR 0014 records the work-state layers and the promotion path.
- Validator detects a stale self-sync copy in payload mode.
- Optional bundle directory `optional/` as a root sibling of `agents/`. It is
  not synced and is exempt from payload genericity.
- Jira optional bundle: `jira-specialist`, `verify-jira-auth`,
  `create-jira-issue`, `enrich-jira-issue`, `review-jira-issue`,
  `triage-jira-issue`, a conventions reference, and prompts.
- GitLab optional bundle: `gitlab-specialist`, `verify-gitlab-auth`,
  `create-merge-request`, `update-merge-request`, `review-merge-request`, a
  conventions reference, a merge-request template, and prompts.
- ADR 0015 records the optional bundle boundary.
- Group A is the Jira and GitLab bundles. Group C keeps `snyk-renovate`
  dependency-update triage out for now.

### Changed

- The validator scans `optional/` for layout, naming, frontmatter, lists,
  references, and secrets, but skips genericity and self-sync.
- `sync-agents` states that `optional/` is not installed automatically.
- `CONTRIBUTING.md`, `README.md`, and the naming rule document the optional
  boundary.

- `markdown.rule.md` now points at the canonical standards instead of repeating
  them.
- `conduct-interview` now supports specification review, repository grounding,
  agreed-text recast, and durable decisions.
- `git-workflow.rule.md` now routes worktree work to the `create-worktree`
  skill.
- AGENTS and README now document the context, plan, and session layers.
- Prompt references now use the `.prompt.md` suffix everywhere.
- Agent and skill names now match their directories.
- Shell command examples no longer contain repository-specific commands.

### Deprecated

### Removed

- `mode` from frontmatter. Three-way merge provides create-once semantics.

### Fixed

- A merge conflict no longer leaves conflict markers in the consumer's file.
- A rename removes the source directory when the move leaves it empty.
- The recorded commit advances only when the payload changes, so a sync commit
  can no longer invalidate the commit it just recorded.
- The sync skill states where the upstream URL comes from on a first run, skips
  the base check when there is no base, and defines the candidate path set as
  the union of payload and on-disk paths.
