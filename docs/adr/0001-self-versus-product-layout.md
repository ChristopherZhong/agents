# 0001 — Self versus product layout

**Status:** Accepted · 2026-11-22

## Context

The repository both defines conventions and must follow them. Without a
boundary, the repository's own guidance and the distributable content blur
together.

## Decision

`/AGENTS.md` and `/.agents/` are this repository's own assets. `/agents/` is the
payload — the only distributable surface.

## Consequences

- The boundary is a single directory, easy to reason about.
- Self-hosting becomes possible: the repository consumes its own payload.
- Every asset exists twice in-tree: source and generated copy.

## Alternatives rejected

A flat repository with no separation. Naming the payload directory something
other than `agents/`.
