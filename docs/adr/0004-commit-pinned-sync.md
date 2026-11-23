# 0004 — Commit-pinned, versionless sync

**Status:** Accepted · 2026-11-22

## Context

A file cannot contain the hash of the commit that contains it. Semantic versions
require tags, a release process, and an immutable-tag policy.

## Decision

There are no versions and no tags. A consumer records the upstream commit it
last synced from in `.agents/config.yaml`. Update detection compares that commit
to upstream HEAD.

## Consequences

- No release ceremony, no tag immutability governance, no stamping.
- "What changed" is answered by `git log <commit>..HEAD`.
- A broken upstream HEAD reaches consumers immediately; upstream must stay green.

## Alternatives rejected

Semantic versions with tags. A two-commit stamp-then-tag dance.
