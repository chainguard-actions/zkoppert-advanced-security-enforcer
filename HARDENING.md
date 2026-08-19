<!-- markdownlint-disable -->

# Hardening Report: zkoppert--advanced-security-enforcer/v2.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **zkoppert--advanced-security-enforcer/v2.0.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple files reference actions and Docker images by mutable tags instead of full 40-character SHA commit digests, making them vulnerable to supply-chain attacks.

action.yml: `image: 'docker://ghcr.io/zkoppert/advanced-security-enforcer:v2'` — Docker image uses tag `:v2` instead of a SHA digest.

.github/workflows/codeql-analysis.yml:
  - `uses: actions/checkout@v4` (line 27)
  - `uses: github/codeql-action/init@v2` (line 30)
  - `uses: github/codeql-action/autobuild@v2` (line 34)
  - `uses: github/codeql-action/analyze@v2` (line 37)

.github/workflows/docker-image.yml:
  - `uses: actions/checkout@v4` (line 17)

.github/workflows/linter.yml:
  - `uses: actions/checkout@v4` (line 25)
  - `uses: docker://ghcr.io/super-linter/super-linter:latest` (line 31) — mutable `:latest` tag

.github/workflows/python-package.yml:
  - `uses: actions/checkout@v4` (line 18)
  - `uses: actions/setup-python@v4` (line 20)

.github/workflows/release-drafter.yml:
  - `uses: release-drafter/release-drafter@v5` (line 13)

Locations:

- `action.yml:8`
- `.github/workflows/codeql-analysis.yml:27`
- `.github/workflows/codeql-analysis.yml:30`
- `.github/workflows/codeql-analysis.yml:34`
- `.github/workflows/codeql-analysis.yml:37`
- `.github/workflows/docker-image.yml:17`
- `.github/workflows/linter.yml:25`
- `.github/workflows/linter.yml:31`
- `.github/workflows/python-package.yml:18`
- `.github/workflows/python-package.yml:20`
- `.github/workflows/release-drafter.yml:13`

### missing-permissions (severity: medium)

Four workflow files have no top-level `permissions:` block and no job-level `permissions:` block on any of their jobs. Without explicit permissions, workflows run with the default (often broad) token permissions, violating the principle of least privilege.

- .github/workflows/docker-image.yml: no permissions declared anywhere
- .github/workflows/linter.yml: no permissions declared anywhere
- .github/workflows/python-package.yml: no permissions declared anywhere
- .github/workflows/release-drafter.yml: no permissions declared anywhere

Locations:

- `.github/workflows/docker-image.yml:1`
- `.github/workflows/linter.yml:1`
- `.github/workflows/python-package.yml:1`
- `.github/workflows/release-drafter.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all unpinned action/image references by resolving real commit SHAs and container digests: (1) action.yml: pinned ghcr.io/zkoppert/advanced-security-enforcer:v2 to sha256 digest while preserving docker:// scheme and tag inline. (2) codeql-analysis.yml: pinned actions/checkout@v4 → SHA 11d5960a, github/codeql-action/init|autobuild|analyze@v2 → SHA b8d3b6e8. (3) docker-image.yml: pinned actions/checkout@v4 → SHA 11d5960a; added top-level permissions: {}. (4) linter.yml: pinned actions/checkout@v4 → SHA 11d5960a, pinned docker://ghcr.io/super-linter/super-linter:latest with sha256 digest inline; added top-level permissions: {} and job-level contents: read. (5) python-package.yml: pinned actions/checkout@v4 → SHA 11d5960a, actions/setup-python@v4 → SHA 7f4fc3e2; added top-level permissions: {} and job-level contents: read. (6) release-drafter.yml: pinned release-drafter/release-drafter@v5 → SHA 09c613e2; added top-level permissions: {} and job-level contents: write + pull-requests: read (minimum needed for release drafting).

