# 0006 — `AGENTS.md` only

**Status:** Accepted · 2026-11-22

## Context

Harnesses disagree on instruction file names: `CLAUDE.md`, `.cursor/rules/`,
`copilot-instructions.md`, `GEMINI.md`, and others.

## Decision

Ship `AGENTS.md` only. Generate no harness-specific files.

## Consequences

- One instruction file, nothing to drift.
- Harnesses that do not read `AGENTS.md` will not auto-discover it; a user can
  add a pointer manually.
- The support matrix must record which harnesses are verified.

## Alternatives rejected

Pointer shims. Mirrored copies.
