# Changelog

Notable changes to the payload. Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

This project does not use semantic versions. Consumers pin a commit; see
`docs/adr/0004-commit-pinned-sync.md`.

## Unreleased

### Added

- Initial payload: 5 rules, 11 skills, 9 prompts, 5 agents, and
  `scripts/validate.py`.
- `sync-agents` skill and `agents-maintainer` agent.
- Governance: `CONTRIBUTING.md`, `SECURITY.md`, `docs/adr/`, support matrix,
  and non-goals.

### Changed

- Prompt references now use the `.prompt.md` suffix everywhere.
- Agent and skill names now match their directories.
- Shell command examples no longer contain repository-specific commands.

### Deprecated

### Removed

- `mode` from frontmatter. Three-way merge provides create-once semantics.

### Fixed
