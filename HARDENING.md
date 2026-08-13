<!-- markdownlint-disable -->

# Hardening Report: 3ru--gpt-translate/v1.2.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **3ru--gpt-translate/v1.2.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Two `uses:` references in the workflow use mutable tag or branch refs instead of pinned 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if the referenced tag or branch is moved or compromised.

- `actions/checkout@v3` (line 13) — mutable tag `v3`
- `3ru/gpt-translate@master` (line 18) — mutable branch `master`

Both should be replaced with their full 40-character commit SHA, e.g. `actions/checkout@<sha> # v3`.

Locations:

- `.github/workflows/gpt-translate.yml:13`
- `.github/workflows/gpt-translate.yml:18`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/gpt-translate.yml` has no top-level `permissions:` key and the single job `gpt_translate` also has no `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions (which may be `write-all` for older repositories), granting broader access than necessary. A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or job level.

Locations:

- `.github/workflows/gpt-translate.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned `actions/checkout@v3` to full SHA `f43a0e5ff2bd294095638e18286ca9a3d1956744 # v3`. 2. Pinned `3ru/gpt-translate@master` to full SHA `d36d569b15411b6e6f727b99c051c443b1b02458 # master`. 3. Added top-level `permissions:` block with `contents: write` and `pull-requests: write` — the minimum permissions needed for the GPT Translate action to commit translated files and interact with pull requests.

