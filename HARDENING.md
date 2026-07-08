<!-- markdownlint-disable -->

# Hardening Report: supercharge--mongodb-github-action/1.12.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **supercharge--mongodb-github-action/1.12.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All workflow files use mutable tag-based refs instead of pinned SHA commits for external actions. Specifically: actions/checkout@v4, actions/setup-node@v4, and krzema12/github-actions-typing@v1 are all unpinned. A compromised or malicious update to any of these tags would automatically affect all workflow runs.

Locations:

- `.github/workflows/main.yml:14`
- `.github/workflows/test-auth.yml:19`
- `.github/workflows/test-auth.yml:29`
- `.github/workflows/test-replica-set.yml:20`
- `.github/workflows/test-replica-set.yml:30`
- `.github/workflows/test-replica-set.yml:56`
- `.github/workflows/test-replica-set.yml:66`
- `.github/workflows/test-single-instance.yml:19`
- `.github/workflows/test-single-instance.yml:29`
- `.github/workflows/test-single-instance.yml:52`
- `.github/workflows/test-single-instance.yml:62`
- `.github/workflows/validate-action-typings.yml:12`
- `.github/workflows/validate-action-typings.yml:13`

### missing-permissions (severity: medium)

None of the workflow files define a top-level or job-level permissions: block. Without explicit permissions, workflows inherit the default repository permissions (which may include write access to contents, packages, etc.), violating the principle of least privilege. Affected files: main.yml, test-auth.yml, test-replica-set.yml, test-single-instance.yml, validate-action-typings.yml.

Locations:

- `.github/workflows/main.yml:1`
- `.github/workflows/test-auth.yml:1`
- `.github/workflows/test-replica-set.yml:1`
- `.github/workflows/test-single-instance.yml:1`
- `.github/workflows/validate-action-typings.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 5 workflow files: (1) Pinned all mutable action refs to full commit SHAs — actions/checkout@v4 → SHA 34e114876b0b11c390a56381ad16ebd13914f8d5, actions/setup-node@v4 → SHA 49933ea5288caeca8642d1e84afbd3f7d6820020, krzema12/github-actions-typing@v1 → SHA 21db25f90324def9328034891ea446b023b8ea77 — with tag comments preserved for readability. (2) Added top-level `permissions: {}` to all 5 workflow files (main.yml, test-auth.yml, test-replica-set.yml, test-single-instance.yml, validate-action-typings.yml) to enforce least-privilege access.

