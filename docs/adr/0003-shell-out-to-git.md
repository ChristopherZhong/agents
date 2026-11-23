# 0003 — Shell out to git

**Status:** Accepted · 2026-11-22

## Context

Sync needs base content, content integrity, rename detection, and three-way
merging. All four are git primitives.

## Decision

Use git commands for all four. Do not reimplement any of them.

## Consequences

- Git becomes a hard dependency. It already is: every consumer is a git
  repository.
- Merge behavior matches what developers expect.
- No diff or merge library to audit or pin.

## Alternatives rejected

In-process diff and merge libraries. Vendored copies of the base.
