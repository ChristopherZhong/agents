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
- Validator detects a stale self-sync copy in payload mode.

### Changed

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
