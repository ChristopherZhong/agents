# Contributing

## What the product is

`agents/` is the core product. `optional/` holds opt-in bundles for a named
platform or stack. Everything else — `README.md`, `docs/`, `/.agents/`,
`/AGENTS.md` — supports them.

A change that does not affect `agents/` or `optional/` does not reach consumers.

## Rules that cannot be broken

### No repository-specific text

Nothing under `agents/` may name a repository, host, organization, product,
technology stack, or directory belonging to one consumer. Write "this
repository", not a name.

`optional/` may name a platform or a stack because the consumer opts in
explicitly. It still must not name a consumer's repository, host, organization,
product, or project key. Write "the project key", not a value.

The validator fails on a denylist for `agents/`. A passing run is necessary, not
sufficient. Review the diff for anything a consumer would find irrelevant.

### One file per rule

Each rule lives in exactly one file under `agents/rules/`. Do not split a rule
across files and do not duplicate it in `AGENTS.md`.

### References use real paths

Skill and agent files reference prompts as `.agents/prompts/<name>.prompt.md`.
The validator checks that referenced paths exist.

### Naming

Follow `.agents/rules/naming-conventions.rule.md`:

- Skills: `<verb>-<noun>`
- Agents: `<workflow>-<actor>.agent.md`
- Prompts: `<descriptive-name>.prompt.md`
- Rules: `<topic>.rule.md`
- Reference documents: `<topic>.reference.md` under `agents/references/`

The same patterns apply under `optional/`. An optional asset keeps the same
relative path when a consumer copies it into `.agents/`.

### No declared state

Do not add a `mode` field, an id, or any other state marker to frontmatter. A
file's state is derived from presence at the recorded commit, at HEAD, and on
disk. The validator rejects `mode`.

## Adding or changing an asset

For a core asset:

1. Edit or add files under `agents/`.
1. Run `python3 .agents/scripts/validate.py --strict`.
1. Commit the payload: `feat: add <asset> to the payload`.
1. Run the `sync-agents` skill to refresh `/.agents/` and `/AGENTS.md`.
1. Commit the self-synced copy: `chore: self-sync .agents`.

For an optional bundle:

1. Edit or add files under `optional/`.
1. Keep the bundle self-contained. A core asset must not reference it.
1. Run `python3 .agents/scripts/validate.py --strict`. The validator checks
   optional naming, frontmatter, and references, but skips genericity.
1. Do not self-sync it. Optional assets are copied by the consumer.
1. Commit the bundle: `feat: add <platform> optional bundle`.

Steps 3 and 4 for a core asset are separate commits because sync reads the
payload from a commit. See `docs/adr/0004-commit-pinned-sync.md`.

## Deprecating an asset

Removing a file from `agents/` prompts every consumer to delete or exclude it.
Warn first:

1. Add a `Deprecated` entry to `CHANGELOG.md` naming the asset and the reason.
1. Keep the asset for at least one subsequent merge to `main`.
1. Remove it and add a `Removed` entry.

Never remove an asset and add its replacement in the same merge unless the
replacement has an identical purpose and the changelog says so.

## Commit messages

Conventional Commits. See `.agents/rules/git-workflow.rule.md`.

## Review

Do not merge a payload change without running the validator and the self-sync.
Both are cheap and both catch the two failure modes that matter: repository
specific text and a stale generated copy.
