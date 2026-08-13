<!-- markdownlint-disable -->

# Hardening Report: 3ru--gpt-translate/v1.2.0-beta

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **3ru--gpt-translate/v1.2.0-beta** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses action references pinned to mutable tags/branches instead of immutable 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the referenced tag or branch is updated with malicious code. Failing references:
- `actions/checkout@v3` (tag, not a SHA)
- `3ru/gpt-translate@master` (branch, not a SHA)
These should be pinned to full SHA digests, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3`.

Locations:

- `.github/workflows/gpt-translate.yml:13`
- `.github/workflows/gpt-translate.yml:17`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the job `gpt_translate` also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the default repository permissions (which may include broad write access). A minimal `permissions:` block should be added — for example `permissions: contents: read` — to follow the principle of least privilege.

Locations:

- `.github/workflows/gpt-translate.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both findings in .github/workflows/gpt-translate.yml: (1) Pinned actions/checkout@v3 to SHA a37ce9120846195fa4ece8f58b268e6043cb2f26 and 3ru/gpt-translate@master to SHA d36d569b15411b6e6f727b99c051c443b1b02458, preserving the original tag/branch as inline comments. (2) Added a top-level `permissions: contents: read` block to enforce least-privilege access.

