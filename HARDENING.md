<!-- markdownlint-disable -->

# Hardening Report: Azure--k8s-bake/v4.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Azure--k8s-bake/v4.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `Azure/k8s-lint@v4` — a mutable tag reference rather than a full 40-character commit SHA. If the tag is moved or the repository is compromised, the action could execute arbitrary code in CI. All five occurrences reference the same unpinned tag.

Locations:

- `.github/workflows/integration-tests.yaml:35`
- `.github/workflows/integration-tests.yaml:52`
- `.github/workflows/integration-tests.yaml:64`
- `.github/workflows/integration-tests.yaml:77`
- `.github/workflows/integration-tests.yaml:89`

### missing-permissions (severity: medium)

These workflow files have no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, workflows inherit the default repository token permissions (which may include write access), violating the principle of least privilege.

Locations:

- `.github/workflows/defaultLabels.yml:1`
- `.github/workflows/integration-tests.yaml:1`
- `.github/workflows/prettify-code.yml:1`
- `.github/workflows/unit-tests.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 5 occurrences of unpinned `Azure/k8s-lint@v4` in integration-tests.yaml by replacing with the full commit SHA `e4234c50ea835112e72b145bdecd00a94bad42fd` (keeping `# v4` comment for readability). Added `permissions: {}` top-level block to all 4 workflow files: integration-tests.yaml, defaultLabels.yml, prettify-code.yml, and unit-tests.yml.

