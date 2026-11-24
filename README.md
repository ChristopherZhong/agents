# agents

A harness of agent conventions that any repository can sync.

`agents` holds rules, skills, prompts, and agent definitions that are useful in
any repository, plus the procedure for installing and updating them. A
repository adopts them by pointing its agent at this one.

## Start here

Paste this into your agent. The copy button is at the top right of the block.

```text
Onboard this repository using the agents harness.

Upstream: https://github.com/ChristopherZhong/agents

1. Clone the upstream repository into a temporary directory outside this one.
2. Read agents/skills/sync-agents/SKILL.md and follow it exactly.
3. Ask me before writing any file. Stop if any step is ambiguous.

Do not commit anything.

When you finish, run .agents/scripts/validate.py and report its output, the
files you created or changed, and anything you had to infer.
```

On a repository with no `.agents/` directory, that is a first run: files are
created. On a repository that already syncs, it is an update: changes are
merged.

The skill is the procedure. There is no binary to install.

## What gets installed

| From `agents/` | To the consumer |
|---|---|
| `AGENTS.md` | `AGENTS.md` |
| `rules/` | `.agents/rules/` |
| `skills/` | `.agents/skills/` |
| `prompts/` | `.agents/prompts/` |
| `agents/` | `.agents/agents/` |
| `scripts/validate.py` | `.agents/scripts/validate.py` |

A consumer's own files in `.agents/` are never touched. Only paths that exist
in the payload are managed.

## How sync behaves

- Pinned to a commit, not a version. The consumer records the commit it last
  synced from in `.agents/config.yaml`.
- Three-way merged. Local edits survive; upstream changes apply around them.
- Never destructive. Ambiguous cases are presented as decisions, not guesses.

## Layout

| Path | Role |
|---|---|
| `agents/` | The payload — the product |
| `.agents/` | This repository's own copy, produced by self-sync |
| `docs/` | Governance, decisions, support matrix |

## Status

No CLI. No versioned releases. The procedure is prose plus git.

## License

Apache-2.0 covers this repository. Files copied into another repository are
governed by that repository's own license.
