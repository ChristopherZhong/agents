# 0005 — No placeholders

**Status:** Accepted · 2026-11-22

## Context

Templates wanted repository names injected. That required a rendering step, a
placeholder schema, and a way to distinguish a placeholder change from a local
edit.

## Decision

Payload text is generic: "this repository", "the default branch".
Repository-specific content is appended to `AGENTS.md` by the consumer.

## Consequences

- No rendering step and no `*.tmpl` file kind.
- The "placeholder changed or file edited?" ambiguity disappears.
- Every consumer's `AGENTS.md` diverges, so upstream edits there may conflict.

## Alternatives rejected

`{{project_name}}` placeholders. A separate `local.md` indirection.
