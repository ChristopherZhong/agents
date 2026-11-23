# 0002 — Tree-derived ownership with three-way merge

**Status:** Accepted · 2026-11-22

## Context

Consumers already have `.agents/` content, and much of it is their own. Sync
must distinguish managed files from repository-owned files.

## Decision

Ownership is derived from the payload tree: a path is managed if and only if it
exists in `agents/`. Sync classifies each path by presence at the recorded
commit, at HEAD, and on disk, then applies the matching action.

## Consequences

- Repository-owned files are invisible to sync, so no manifest is needed.
- State is required: the consumer records the commit it last synced from.
- Both-changed files can conflict and need a decision.

## Alternatives rejected

A manifest enumerating every managed file. Managed-block markers inside files.
Stable ids in frontmatter.
