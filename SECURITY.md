# Security Policy

## Scope

This repository distributes files that other repositories copy into their own
trees. The relevant threat is a consumer receiving content they did not review.

## Design property

Sync is write-only. It reads and writes files; it never executes fetched
content. Scripts such as `.agents/scripts/validate.py` run only when a human
invokes them.

No consumer runs code from this repository automatically.

## Reporting

Report suspected vulnerabilities privately to the maintainer listed in
`CODEOWNERS`. Do not open a public issue.

Include the affected path, what a consumer would do differently as a result,
and whether the consumer must act.

## What counts

- Content that would cause a consumer to run an unexpected command
- A path that escapes the repository root during sync
- A dependency that introduces execution during validation
- Secrets committed to the payload

## What does not

- The absence of a CLI or a release process
- Merge conflicts, which are expected and resolved by a human
