# 0014 — Work state layers by durability

**Status:** Accepted · 2026-11-25

## Context

Agents need three kinds of working memory: scratch state for the current task,
durable facts for future tasks, and plans for non-trivial work. One notes file
mixes transient and durable content. Committing everything adds noise to
history. Keeping nothing loses decisions.

## Decision

Use three layers:

| Layer | Path | Tracked |
|---|---|---|
| Session | `.agents/sessions/` | No |
| Context | `.agents/context/` | Yes |
| Plans | `.agents/docs/` | Yes when useful |

A session note starts the task. A verified, durable fact moves to context. A
durable decision that meets the ADR conditions moves to `docs/adr/`. A plan
stays in `.agents/docs/` when it needs review or history.

## Consequences

- The repository has a clear promotion path for working memory.
- Consumers must ignore `.agents/sessions/`.
- Context and plan directories are optional and created on demand.
- The payload does not ship these directories. It ships the convention.

## Alternatives rejected

- **One notes file:** Transient and durable content mix, and history becomes
  noisy.
- **Commit every session note:** The history fills with scratch state.
- **Keep no working memory:** Decisions and verified facts are lost between
  tasks.
