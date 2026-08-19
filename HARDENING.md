<!-- markdownlint-disable -->

# Hardening Report: zkoppert--advanced-security-enforcer/v1.0.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **zkoppert--advanced-security-enforcer/v1.0.3** was hardened automatically. 8 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml uses a mutable Docker image tag instead of a SHA digest: `image: 'docker://ghcr.io/zkoppert/advanced-security-enforcer:v1'`. This is vulnerable to supply-chain attacks as the tag can be silently updated to point to a different image.

Locations:

- `action.yml:7`

### unpinned-uses (severity: high)

Multiple workflow steps use mutable tag/version refs instead of full 40-character SHA commit hashes, making them vulnerable to supply-chain attacks. Failing references: `actions/checkout@v2`, `github/codeql-action/init@v1`, `github/codeql-action/autobuild@v1`, `github/codeql-action/analyze@v1`.

Locations:

- `.github/workflows/codeql-analysis.yml:34`
- `.github/workflows/codeql-analysis.yml:39`
- `.github/workflows/codeql-analysis.yml:46`
- `.github/workflows/codeql-analysis.yml:58`

### unpinned-uses (severity: high)

Workflow step uses a mutable tag ref instead of a full 40-character SHA commit hash: `actions/checkout@v2`.

Locations:

- `.github/workflows/docker-image.yml:14`

### unpinned-uses (severity: high)

Workflow steps use mutable tag/version refs instead of full 40-character SHA commit hashes: `actions/checkout@v2.3.4` and `docker://ghcr.io/github/super-linter:latest` (mutable `:latest` tag).

Locations:

- `.github/workflows/linter.yml:30`
- `.github/workflows/linter.yml:36`

### unpinned-uses (severity: high)

Workflow step uses a mutable tag ref instead of a full 40-character SHA commit hash: `release-drafter/release-drafter@v5`.

Locations:

- `.github/workflows/release-drafter.yml:11`

### permissions (severity: medium)

missing-permissions: The workflow has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially broad) permissions.

Locations:

- `.github/workflows/docker-image.yml:1`

### permissions (severity: medium)

missing-permissions: The workflow has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially broad) permissions.

Locations:

- `.github/workflows/linter.yml:1`

### permissions (severity: medium)

missing-permissions: The workflow has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially broad) permissions.

Locations:

- `.github/workflows/release-drafter.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, permissions

**Notes:**

Fixed all 8 findings across 5 files:

1. action.yml: Pinned `docker://ghcr.io/zkoppert/advanced-security-enforcer:v1` to `docker://ghcr.io/zkoppert/advanced-security-enforcer:v1@sha256:d7a0fc0a3a8732d80da177df5be460c4e4dc0e33d07c9ffaff23945c0a1cc6e7` (preserved docker:// scheme and :v1 tag inline).

2. .github/workflows/codeql-analysis.yml: Pinned 4 action refs to full SHAs — actions/checkout@v2 → @0717577d45739eb3c851188b29f50ed6c0b2194e, github/codeql-action/init@v1 → @231aa2c8a89117b126725a0e11897209b7118144, github/codeql-action/autobuild@v1 → same SHA, github/codeql-action/analyze@v1 → same SHA. (Already had job-level permissions block.)

3. .github/workflows/docker-image.yml: Pinned actions/checkout@v2 → @0717577d45739eb3c851188b29f50ed6c0b2194e; added top-level `permissions: contents: read`.

4. .github/workflows/linter.yml: Pinned actions/checkout@v2.3.4 → @5a4ac9002d0be2fb38bd78e4b4dbde5606d7042f; pinned docker://ghcr.io/github/super-linter:latest to digest sha256:b723c817982b85f6f98c9c24a653f9f760bf5941577f5ea9532d31bd89aa8823 (tag kept inline); added top-level `permissions: contents: read`.

5. .github/workflows/release-drafter.yml: Pinned release-drafter/release-drafter@v5 → @09c613e259eb8d4e7c81c2cb00618eb5fc4575a7; added top-level `permissions: contents: write, pull-requests: read` (minimum needed for release-drafter to create/update draft releases).

