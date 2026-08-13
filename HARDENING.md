<!-- markdownlint-disable -->

# Hardening Report: 3ru--gpt-translate/v1.1.12

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **3ru--gpt-translate/v1.1.12** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file references two Actions using mutable refs instead of full 40-character commit SHA digests, making the workflow vulnerable to supply-chain attacks if those refs are moved or overwritten:
- `actions/checkout@v3` (line 13) — uses a version tag
- `3ru/gpt-translate@master` (line 18) — uses a branch name
Both should be pinned to their full SHA digest (e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3`).

Locations:

- `.github/workflows/gpt-translate.yml:13`
- `.github/workflows/gpt-translate.yml:18`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/gpt-translate.yml` has no top-level `permissions:` key and the only job (`gpt_translate`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or on the job.

Locations:

- `.github/workflows/gpt-translate.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/gpt-translate.yml: (1) Pinned actions/checkout@v3 to full SHA f43a0e5ff2bd294095638e18286ca9a3d1956744 and 3ru/gpt-translate@master to full SHA d36d569b15411b6e6f727b99c051c443b1b02458, preserving the original ref as a comment. (2) Added top-level `permissions: contents: read` block to restrict the workflow token to the minimum required permissions.

