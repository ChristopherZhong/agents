# 0011 — Payload mirrors the target

**Status:** Accepted · 2026-11-22

## Context

A `templates/` wrapper hid what landed where and added an indirection with no
behavior.

## Decision

`agents/X` maps to `.agents/X`. `agents/AGENTS.md` maps to `/AGENTS.md`. Nothing
else is special.

## Consequences

- Reading `agents/` tells you exactly what a consumer receives.
- No file list is needed; the tree is the list.
- Only `AGENTS.md` needs a mapping rule, because it lands at the root.

## Alternatives rejected

A `templates/` wrapper. An explicit `files:` list.
