# 0009 — Git rename detection

**Status:** Accepted · 2026-11-22

## Context

Renames must be detected so history is preserved rather than deleted and
recreated.

## Decision

Use `git diff --name-status -M`. Carry no ids in the payload.

## Consequences

- No metadata to author or maintain.
- A rename with heavy edits may be missed and degrade to delete plus add; the
  skill must say so.
- Frontmatter stays as it is today.

## Alternatives rejected

Stable ids in frontmatter. A central id map.
