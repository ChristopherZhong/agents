# Sync Case Evidence

Every branch of the classification table was executed against fixtures, not
just reasoned about. This page records what ran and what it produced.

The sync procedure is prose, so it cannot be unit-tested directly. What can be
tested is whether the commands it prescribes do what it claims. Each case below
runs those commands and asserts the result.

## Fixture

A scratch upstream repository and a scratch consumer repository, both real git
repositories.

| Role | Contents |
|---|---|
| Upstream, commit A | Eight payload files: `AGENTS.md`, six rules, one skill |
| Upstream, commit B | Adds two rules, deletes one, modifies three, renames one skill |
| Consumer | Synced from A, with deliberate local divergence |
| `config.yaml` | `commit: A`, `exclude: [rules/excluded.rule.md]` |

The consumer diverges in five ways: an edit to a file upstream also edits, a
conflicting edit to a different file, a local file at a path upstream adds, a
deleted file upstream still has, and an excluded path upstream modifies.

## Results

| # | Case | Expected | Observed |
|---|---|---|---|
| 3 | New upstream file | create | created |
| 5 | Collision | ask | ask — collision |
| 7 | Removed upstream | ask | ask — delete or exclude |
| 8 | Deleted locally | ask | ask — restore or exclude |
| 9 | Unchanged both sides | no-op | no-op, twice |
| 12 | Both changed, no overlap | merge | merged clean, both edits present |
| 12 | Both changed, overlap | ask | conflict, local file untouched |
| — | Rename upstream | move and merge | `R073` detected, moved, merged clean |
| — | Excluded path | silent | untouched and never reported |

13 of 13 assertions passed.

## What the fixtures caught

### Conflict markers were written to the consumer's file

`git merge-file` rewrites its first argument. The skill said "stop without
writing" while passing the local file as that argument, so a conflict would have
left `<<<<<<<` markers in the consumer's tree — the exact opposite of the
promise.

Fixed: merge into a scratch copy, and move it over the local file only when the
exit status is 0.

### Renames left an empty directory

Moving the file carried the content to the new path but left the old directory
on disk. Git does not track empty directories, so nothing reported it.

Fixed: remove the source directory when the move leaves it empty.

### The recorded commit invalidated itself

Found separately, during the first real sync: a sync commit writes only
`.agents/`, which advances HEAD without changing the payload. Recording HEAD
unconditionally made every sync produce a config-only commit, forever.

Fixed: advance the recorded commit only when `git diff --quiet <old> <new> --
agents/` reports a difference.

## Not covered

- Two upstream files colliding with each other after the mapping.
- A rename whose destination already exists locally.
- An excluded path that is also deleted locally.
- Interrupted writes.

These are listed so the gap is visible rather than implied to be tested.

## Reproducing

The harness lives outside the repository and is not shipped. To rebuild it,
create an upstream repository with a `agents/` payload, commit a base, advance
it with an add, a delete, a modify, and a `git mv`, then run the commands from
`.agents/skills/sync-agents/SKILL.md` against a consumer synced from the base.
