# 0010 — Mixed `.agents/` directory

**Status:** Accepted · 2026-11-22

## Context

Consumers have both harness assets and their own rules, skills, and agents.
Forcing a split would fight existing repository layouts.

## Decision

`.agents/` is a shared directory. Sync manages only the paths present in the
payload.

## Consequences

- Harness and repository-owned assets coexist without extra structure.
- A name collision is possible and resolves through the collision rules.
- The directory is not a reliable indicator of what is managed; the payload is.

## Alternatives rejected

Separate directories for harness and local assets.
