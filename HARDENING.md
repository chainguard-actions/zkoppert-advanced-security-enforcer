<!-- markdownlint-disable -->

# Hardening Report: zkoppert--advanced-security-enforcer/v2.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **zkoppert--advanced-security-enforcer/v2.0.0** was hardened automatically. 9 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yml uses a mutable Docker image tag ('docker://ghcr.io/zkoppert/advanced-security-enforcer:v1') instead of a SHA digest. This is vulnerable to supply-chain attacks because the tag can be silently updated to point to a different image.

Locations:

- `action.yml:8`

### unpinned-uses (severity: high)

Multiple workflow files reference actions by mutable tags/versions instead of full 40-character commit SHAs. Affected references: actions/checkout@v2, github/codeql-action/init@v1, github/codeql-action/autobuild@v1, github/codeql-action/analyze@v1.

Locations:

- `.github/workflows/codeql-analysis.yml:27`
- `.github/workflows/codeql-analysis.yml:30`
- `.github/workflows/codeql-analysis.yml:33`
- `.github/workflows/codeql-analysis.yml:36`

### unpinned-uses (severity: high)

docker-image.yml references actions/checkout@v2 — a mutable tag instead of a full 40-character commit SHA.

Locations:

- `.github/workflows/docker-image.yml:14`

### unpinned-uses (severity: high)

linter.yml references actions/checkout@v2.3.4 (mutable tag) and uses docker://ghcr.io/github/super-linter:latest (mutable Docker image tag) instead of pinned SHA references.

Locations:

- `.github/workflows/linter.yml:27`
- `.github/workflows/linter.yml:32`

### unpinned-uses (severity: high)

release-drafter.yml references release-drafter/release-drafter@v5 — a mutable tag instead of a full 40-character commit SHA.

Locations:

- `.github/workflows/release-drafter.yml:12`

### unpinned-uses (severity: high)

Root codeql.yml references actions/checkout@v2, github/codeql-action/init@v1, github/codeql-action/autobuild@v1, and github/codeql-action/analyze@v1 — all mutable tags instead of full 40-character commit SHAs.

Locations:

- `codeql.yml:18`
- `codeql.yml:22`
- `codeql.yml:27`
- `codeql.yml:31`

### missing-permissions (severity: medium)

docker-image.yml has no top-level 'permissions:' key and the single job ('build') also has no job-level 'permissions:' key. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially broad) permissions.

Locations:

- `.github/workflows/docker-image.yml:1`

### missing-permissions (severity: medium)

linter.yml has no top-level 'permissions:' key and the single job ('build') also has no job-level 'permissions:' key. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially broad) permissions.

Locations:

- `.github/workflows/linter.yml:1`

### missing-permissions (severity: medium)

release-drafter.yml has no top-level 'permissions:' key and the single job ('update_release_draft') also has no job-level 'permissions:' key. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially broad) permissions.

Locations:

- `.github/workflows/release-drafter.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 6 unpinned-uses findings and 3 missing-permissions findings:

1. action.yml: Pinned 'docker://ghcr.io/zkoppert/advanced-security-enforcer:v1' to '@sha256:d7a0fc0a3a8732d80da177df5be460c4e4dc0e33d07c9ffaff23945c0a1cc6e7'

2. .github/workflows/codeql-analysis.yml: Pinned actions/checkout@v2 → @0717577d45739eb3c851188b29f50ed6c0b2194e, github/codeql-action/{init,autobuild,analyze}@v1 → @231aa2c8a89117b126725a0e11897209b7118144

3. .github/workflows/docker-image.yml: Pinned actions/checkout@v2 → @0717577d45739eb3c851188b29f50ed6c0b2194e; added 'permissions: {}' top-level block

4. .github/workflows/linter.yml: Pinned actions/checkout@v2.3.4 → @5a4ac9002d0be2fb38bd78e4b4dbde5606d7042f; pinned docker://ghcr.io/github/super-linter:latest to '@sha256:b723c817982b85f6f98c9c24a653f9f760bf5941577f5ea9532d31bd89aa8823'; added 'permissions: {}' top-level block

5. .github/workflows/release-drafter.yml: Pinned release-drafter/release-drafter@v5 → @09c613e259eb8d4e7c81c2cb00618eb5fc4575a7; added minimal permissions (contents: write, pull-requests: read) needed for release drafting

6. codeql.yml: Pinned actions/checkout@v2 → @0717577d45739eb3c851188b29f50ed6c0b2194e; pinned github/codeql-action/{init,autobuild,analyze}@v1 → @231aa2c8a89117b126725a0e11897209b7118144

