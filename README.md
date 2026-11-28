# agents

[![License](https://img.shields.io/github/license/ChristopherZhong/agents)](LICENSE)
[![Last commit](https://img.shields.io/github/last-commit/ChristopherZhong/agents)](https://github.com/ChristopherZhong/agents/commits/main)
[![Requires](https://img.shields.io/badge/requires-git%20%2B%20python%203-informational)](#requirements)
[![Sync](https://img.shields.io/badge/sync-three--way%20merge-blue)](#how-sync-behaves)

A harness of agent conventions that any repository can sync.

`agents` holds rules, reference standards, skills, prompts, and agent
definitions that are useful in any repository, plus the procedure for
installing and updating them. A repository adopts them by pointing its agent at
this one.

`optional/` holds opt-in bundles for a named platform or stack. A bundle keeps
platform-specific workflows out of the generic payload. The consumer copies a
bundle only when it uses that platform or stack.

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

## Requirements

- `git` — clone, diff, and three-way merge.
- Python 3 — the validator. Standard library only, no packages.

## What gets installed

| From `agents/` | To the consumer |
|---|---|
| `AGENTS.md` | `AGENTS.md` |
| `rules/` | `.agents/rules/` |
| `skills/` | `.agents/skills/` |
| `prompts/` | `.agents/prompts/` |
| `agents/` | `.agents/agents/` |
| `references/` | `.agents/references/` |
| `scripts/validate.py` | `.agents/scripts/validate.py` |

A consumer's own files in `.agents/` are never touched. Only paths that exist
in the payload are managed.

`optional/` is not part of this mapping. Sync never installs it. Copy a bundle
into `.agents/` by hand when the repository uses that platform or stack.

The payload does not ship `.agents/context/`, `.agents/docs/`, or
`.agents/sessions/`. The work-state convention creates them on demand. Session
notes are not committed.

## Optional bundles

`optional/` is a sibling of `agents/`. It mirrors the payload structure with
`skills/`, `prompts/`, `agents/`, and `references/`. It is validated for layout,
naming, frontmatter, and references, but it is exempt from the payload
genericity rule. A bundle may name a platform or a stack because the consumer
opts in explicitly.

Available bundles (Group A):

| Bundle | Contents |
|---|---|
| Jira | `jira-specialist`, create, enrich, review, and triage skills, auth check, conventions reference, and prompts |
| GitLab | `gitlab-specialist`, create, update, and review skills, auth check, conventions reference, and prompts |

Deferred bundles:

- Dependency-update merge-request triage (`snyk-renovate`), classified Group C.
- NestJS and Prisma stack skills and agents.
- Generic orchestration and a flow runner.

To opt in:

1. Copy the bundle files from `optional/skills/`, `optional/agents/`,
   `optional/prompts/`, and `optional/references/` into the matching `.agents/`
   directories.
1. Record the project values in `.agents/context/` with the format in
   `.agents/references/context-format.reference.md`. The Jira bundle needs the
   site, cloud ID, project key, and field metadata. The GitLab bundle needs the
   host, project path, default branch, and protected branches.
1. Run `.agents/scripts/validate.py` and confirm the installed tree is valid.

Core assets never reference an optional bundle. An optional asset may reference
a core asset.

## Work state

- `.agents/sessions/` holds active scratch notes. Do not commit them. Add the
  directory to the repository ignore file.
- `.agents/context/` holds durable, verified notes about the repository.
- `.agents/docs/` holds plans for non-trivial work.
- Promote a durable decision that meets the ADR conditions to `docs/adr/`.
- Read `.agents/references/work-state.reference.md` before you create or
  update a work-state file.

## How sync behaves

- Pinned to a commit, not a version. The consumer records the commit it last
  synced from in `.agents/config.yaml`.
- Three-way merged. Local edits survive; upstream changes apply around them.
- Never destructive. Ambiguous cases are presented as decisions, not guesses.

## Layout

| Path | Role |
|---|---|
| `agents/` | The payload — the core product |
| `optional/` | Opt-in platform and stack bundles, not synced |
| `.agents/` | This repository's own copy, produced by self-sync |
| `docs/` | Governance, decisions, support matrix |

## Status

No CLI. No versioned releases. The procedure is prose plus git.

## License

Apache-2.0 covers this repository. Files copied into another repository are
governed by that repository's own license.
