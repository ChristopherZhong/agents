# 0015 — Optional bundles for platform and stack assets

**Status:** Accepted · 2026-11-27

## Context

The api-gateway agent tree contains reusable roles that name a platform or a
stack: Jira and GitLab issue I/O, NestJS and Prisma workflows, and a flow
runner. The generic payload rejects those names on purpose. A consumer that uses
Jira should not receive GitLab skills, and a repository that does not use
NestJS should not receive NestJS patterns.

Rejecting the assets entirely loses a real workflow. Putting them in `agents/`
breaks the genericity rule and forces every consumer to carry them.

## Decision

Add a root `optional/` directory as a sibling of `agents/`. It mirrors the
payload layout with `skills/`, `prompts/`, `agents/`, and `references/`.

- Sync does not map `optional/`. It never installs a bundle.
- A consumer copies a bundle into `.agents/` by hand.
- The validator checks optional layout, naming, frontmatter, lists, references,
  and secrets. It skips genericity and self-sync.
- An optional asset may name a platform or a stack. It must not name a
  consumer's repository, host, organization, product, or project key.
- A core asset must not reference an optional asset. An optional asset may
  reference a core asset.
- Project values such as a site, project key, host, or default branch come from
  `.agents/context/` or the user. They are not hard-coded in a bundle.

The first bundles are Jira and GitLab (Group A). Dependency-update triage
(`snyk-renovate`) is classified Group C and kept out. Stack bundles and
orchestration remain deferred.

## Consequences

- The generic payload stays portable and small.
- A consumer opts in with a file copy, not a second sync mechanism.
- The validator has two scopes: the payload with genericity, and optional
  bundles without it.
- An optional bundle maps to the same `.agents/<path>` target when installed, so
  the existing naming and reference rules still apply.
- Core and optional assets can drift apart in style. The shared validator and a
  review of the optional bundle limit that risk.

## Alternatives rejected

- **Put platform assets in `agents/`:** Breaks the genericity rule and the
  consumer contract.
- **Ship a second upstream repository:** Adds a second pin, a second sync, and a
  version matrix.
- **Ship harness adapters:** Rejected by ADR 0006 and the non-goals. Platform
  assets are not harness assets.
- **Use placeholders for project values:** Rejected by ADR 0005. Project values
  belong in context or in the user request.
