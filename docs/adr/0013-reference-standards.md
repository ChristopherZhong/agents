# 0013 — Standards in a references directory

**Status:** Accepted · 2026-11-25

**Renamed:** The directory `reference/` became `references/` on 2026-11-26. The
decision is unchanged.

## Context

The payload now ships EARS and ASD-STE100 standards, plus skills and agents that
use them. Standards are long. Rules are read on every task. Putting the full
standards in `rules/` would make every task load text that only some tasks need.

## Decision

Ship long-lived standards under `agents/references/`. They map to
`.agents/references/`. Each file uses the `<topic>.reference.md` suffix. Rules
state the obligation and point to the reference file. The validator expects the
directory and the suffix. A workflow loads a reference file only when it needs
it.

## Consequences

- Always-read rules stay short.
- Reference files can be detailed without a context cost on unrelated tasks.
- The payload has one more directory and one more structure check.
- A reference file is not a rule. It does not bind behavior by itself.

## Alternatives rejected

- **Keep standards in `rules/`:** Every task pays the context cost.
- **Inline standards in each skill:** The text duplicates and drifts.
- **Ship no standards:** The review skills have no canonical source.
