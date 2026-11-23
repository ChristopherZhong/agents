# Non-Goals

Explicit scope boundaries. A request outside these is out of scope until a
decision changes them.

## Not an agent runtime

This repository does not run agents. It distributes instructions that agents
read.

## No CLI

There is no `agents` binary. Sync is a procedure executed by an agent. A CLI is
deferred, not rejected.

## No versions or release tags

Consumers pin a commit. There is no semantic versioning, no release process, and
no immutable-tag policy to maintain.

## No harness-specific files

No `CLAUDE.md`, no `.cursor/rules/`, no `copilot-instructions.md`. A user whose
harness does not read `AGENTS.md` may add a pointer manually.

## Not a package manager

No dependency resolution, no transitive assets, and no lockfile beyond
`.agents/config.yaml`.

## No CI workflow shipped

Consumers receive no workflow. Running an agent in CI needs a runner and
credentials, which is out of scope until the CLI exists.

## No automatic execution

Sync never runs fetched content.
