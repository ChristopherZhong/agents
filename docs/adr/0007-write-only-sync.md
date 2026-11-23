# 0007 — Write-only sync

**Status:** Accepted · 2026-11-22

## Context

Sync fetches content from a remote repository. That content is untrusted.

## Decision

Sync reads and writes files. It never executes anything it fetched.

## Consequences

- A compromised upstream cannot execute code in a consumer.
- Helper scripts such as `validate.py` run only when a human invokes them.
- No post-sync hooks.

## Alternatives rejected

Checksum-verified post-sync hooks.
