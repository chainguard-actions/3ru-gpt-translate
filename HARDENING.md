<!-- markdownlint-disable -->

# Hardening Report: 3ru--gpt-translate/v1.2.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **3ru--gpt-translate/v1.2.2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file references two actions with mutable tag/branch refs instead of pinned full SHA digests. `actions/checkout@v3` uses a version tag and `3ru/gpt-translate@master` uses a branch name. Both should be pinned to a full 40-character commit SHA to prevent supply-chain attacks.

Locations:

- `.github/workflows/gpt-translate.yml:13`
- `.github/workflows/gpt-translate.yml:18`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the only job (`gpt_translate`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. A minimal permissions block (e.g. `contents: read`) should be added.

Locations:

- `.github/workflows/gpt-translate.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/gpt-translate.yml: (1) Pinned actions/checkout@v3 to full SHA f43a0e5ff2bd294095638e18286ca9a3d1956744 and 3ru/gpt-translate@master to full SHA d36d569b15411b6e6f727b99c051c443b1b02458, preserving original tags as inline comments. (2) Added top-level `permissions: contents: read` block to enforce least-privilege token access.

