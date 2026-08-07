<!-- markdownlint-disable -->

# Hardening Report: Azure--k8s-bake/v4.1.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Azure--k8s-bake/v4.1.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the single job also has no `permissions:` key. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions, violating least-privilege.

Locations:

- `.github/workflows/integration-tests.yaml:1`
- `.github/workflows/prettify-code.yml:1`
- `.github/workflows/defaultLabels.yml:1`
- `.github/workflows/unit-tests.yml:1`

### unpinned-uses (severity: high)

The workflow uses `Azure/k8s-lint@v4` (a mutable tag reference) in 5 steps. Mutable tag references can be silently updated to point to different, potentially malicious commits. All `uses:` references should be pinned to a full 40-character commit SHA (e.g. `Azure/k8s-lint@<sha> # v4`). Failing references: line 36 (`Azure/k8s-lint@v4`), line 55 (`Azure/k8s-lint@v4`), line 65 (`Azure/k8s-lint@v4`), line 75 (`Azure/k8s-lint@v4`), line 88 (`Azure/k8s-lint@v4`).

Locations:

- `.github/workflows/integration-tests.yaml:36`
- `.github/workflows/integration-tests.yaml:55`
- `.github/workflows/integration-tests.yaml:65`
- `.github/workflows/integration-tests.yaml:75`
- `.github/workflows/integration-tests.yaml:88`

## Iteration Notes

### Iteration 1

**Fixes applied:** missing-permissions, unpinned-uses

**Notes:**

Fixed all findings: (1) Pinned all 5 occurrences of `Azure/k8s-lint@v4` to full SHA `e4234c50ea835112e72b145bdecd00a94bad42fd # v4` in integration-tests.yaml. (2) Added `permissions: {}` to integration-tests.yaml, prettify-code.yml, and unit-tests.yml (no special permissions needed). Added minimal required permissions (`issues: write`, `pull-requests: write`) to defaultLabels.yml since it uses actions/stale which must label and manage issues/PRs.

