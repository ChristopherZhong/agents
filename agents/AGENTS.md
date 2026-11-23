# Agent Guide

This repository uses the **agents** harness for shared agent conventions.

## Syncing

To create or update this repository's agent assets, load the `sync-agents`
skill from the upstream harness and follow it.

- Upstream location: `.agents/config.yaml` → `agents.upstream`
- Last synced commit: `.agents/config.yaml` → `agents.commit`

Do not hand-edit `.agents/rules/`, `.agents/skills/`, `.agents/prompts/`,
`.agents/agents/`, or `.agents/scripts/` unless you intend to diverge from the
harness. Local changes are preserved by three-way merge, but upstream edits to
the same lines require a decision.

## Where things live

| Path | Contents |
|---|---|
| `.agents/rules/` | Repository conventions, one file per rule |
| `.agents/skills/` | Reusable procedures |
| `.agents/prompts/` | Short user-facing invocations |
| `.agents/agents/` | Agent definitions |
| `.agents/scripts/` | Helper scripts |

## Core rules

Read every file in `.agents/rules/` before acting. Those files are the source
of truth for repository behavior. Do not duplicate them here.

## Uncertainty

If a request is ambiguous, stop and ask. Ask at most three direct questions.
Do not guess, and do not take initiative on ambiguous work.

## Conflict handling

If a requested change would break existing tests, violate a rule in
`.agents/rules/`, or alter existing behavior without approval, stop and explain
the conflict in two or three sentences, then ask one question.

## Repository specifics

Append repository-specific guidance below this heading: purpose, technologies,
layout, and workflows. Upstream has no counterpart for these sections, so sync
will not modify them.
