<!-- markdownlint-disable -->

# Hardening Report: zkoppert--advanced-security-enforcer/v1.0.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **zkoppert--advanced-security-enforcer/v1.0.2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference actions and Docker images by mutable tags/versions instead of full 40-character commit SHAs. This exposes the workflow to supply-chain attacks where a tag can be silently moved to point to malicious code.

- .github/workflows/codeql-analysis.yml: `actions/checkout@v2`, `github/codeql-action/init@v1`, `github/codeql-action/autobuild@v1`, `github/codeql-action/analyze@v1`
- .github/workflows/docker-image.yml: `actions/checkout@v2`
- .github/workflows/linter.yml: `actions/checkout@v2.3.4`, `docker://ghcr.io/github/super-linter:latest` (mutable :latest image tag)
- .github/workflows/release-drafter.yml: `release-drafter/release-drafter@v5`

Locations:

- `.github/workflows/codeql-analysis.yml:36`
- `.github/workflows/codeql-analysis.yml:40`
- `.github/workflows/codeql-analysis.yml:48`
- `.github/workflows/codeql-analysis.yml:57`
- `.github/workflows/docker-image.yml:16`
- `.github/workflows/linter.yml:30`
- `.github/workflows/linter.yml:35`
- `.github/workflows/release-drafter.yml:13`

### missing-permissions (severity: medium)

Three workflow files have no top-level `permissions:` key and no job-level `permissions:` key on any of their jobs. Without explicit permissions, workflows run with the default (often overly broad) token permissions, violating the principle of least privilege.

- .github/workflows/docker-image.yml: no permissions defined at any level
- .github/workflows/linter.yml: no permissions defined at any level
- .github/workflows/release-drafter.yml: no permissions defined at any level

Locations:

- `.github/workflows/docker-image.yml:1`
- `.github/workflows/linter.yml:1`
- `.github/workflows/release-drafter.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 8 unpinned action/image references by resolving full commit SHAs via lookup_action_sha and lookup_container_digest. Added top-level permissions blocks to docker-image.yml (contents: read), linter.yml (contents: read), and release-drafter.yml (contents: write, pull-requests: read). The codeql-analysis.yml already had job-level permissions and only needed the unpinned-uses fix. The super-linter container image was pinned inline as 'docker://ghcr.io/github/super-linter:latest@sha256:...' preserving both the tag and the docker:// scheme.

