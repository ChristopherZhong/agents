# 0008 — Ask, do not guess

**Status:** Accepted · 2026-11-22

## Context

Collisions and merge conflicts need judgment about which differences are
intentional.

## Decision

For ambiguous cases, present a classified comparison and offer exactly one of:
take the payload version, merge the payload with retained local differences, or
exclude the path. If a difference cannot be classified, ask.

## Consequences

- Sync must be agent-driven; a mechanical script cannot do this.
- No silent overwrites in either direction.
- Ambiguous runs pause for a human decision.

## Alternatives rejected

Last-writer-wins. Always-payload-wins.
