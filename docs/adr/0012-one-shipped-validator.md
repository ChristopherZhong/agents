# 0012 — One shipped validator

**Status:** Accepted · 2026-11-22

## Context

Asset layout needs enforcement, and consumers need a way to self-check. Two
overlapping validators would drift.

## Decision

Ship a single `scripts/validate.py`. Standard library only. It detects payload
mode by the presence of `agents/` and runs additional checks there.

## Consequences

- One place to fix bugs; consumers get the same checks.
- A minimal YAML parser is required, which limits `config.yaml` and frontmatter
  to scalars and flat lists.
- No `pip install` anywhere.

## Alternatives rejected

Per-skill validator scripts. Requiring PyYAML.
