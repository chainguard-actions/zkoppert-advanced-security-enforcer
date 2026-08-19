<!-- markdownlint-disable -->

# Hardening Report: zkoppert--advanced-security-enforcer/v1.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **zkoppert--advanced-security-enforcer/v1.0.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference Actions and Docker images using mutable tags or version strings instead of full 40-character SHA commit hashes. This exposes the workflow to supply-chain attacks where a tag can be silently moved to point to malicious code.

Failing references:
- actions/checkout@v2 (mutable tag)
- github/codeql-action/init@v1 (mutable tag)
- github/codeql-action/autobuild@v1 (mutable tag)
- github/codeql-action/analyze@v1 (mutable tag)
- actions/checkout@v2.3.4 (mutable tag)
- docker://ghcr.io/github/super-linter:latest (mutable Docker image tag)
- release-drafter/release-drafter@v5 (mutable tag)

Locations:

- `.github/workflows/codeql-analysis.yml:33`
- `.github/workflows/codeql-analysis.yml:37`
- `.github/workflows/codeql-analysis.yml:44`
- `.github/workflows/codeql-analysis.yml:55`
- `.github/workflows/docker-image.yml:16`
- `.github/workflows/linter.yml:30`
- `.github/workflows/linter.yml:34`
- `.github/workflows/release-drafter.yml:13`

### missing-permissions (severity: medium)

Three workflow files have no top-level `permissions:` key and no job-level `permissions:` key on any of their jobs. Without explicit permissions, GitHub Actions grants the default token permissions (which can be broad, especially write access to contents on older repositories). Each workflow should declare the minimal permissions required.

- docker-image.yml: no permissions declared at top-level or job level
- linter.yml: no permissions declared at top-level or job level
- release-drafter.yml: no permissions declared at top-level or job level

Locations:

- `.github/workflows/docker-image.yml:1`
- `.github/workflows/linter.yml:1`
- `.github/workflows/release-drafter.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 7 unpinned action/image references by resolving them to full 40-character SHA commit hashes using lookup_action_sha and lookup_container_digest. Added minimal permissions blocks to docker-image.yml (contents: read), linter.yml (contents: read), and release-drafter.yml (contents: write). The codeql-analysis.yml already had job-level permissions so only its unpinned uses references were updated. The docker://ghcr.io/github/super-linter:latest image was pinned inline as docker://ghcr.io/github/super-linter:latest@sha256:... preserving the tag and docker:// scheme.

