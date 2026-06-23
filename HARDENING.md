<!-- markdownlint-disable -->

# Hardening Report: zkoppert--advanced-security-enforcer/v2.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **zkoppert--advanced-security-enforcer/v2.0.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml uses a Docker image reference with a mutable tag instead of a SHA digest. The image 'docker://ghcr.io/zkoppert/advanced-security-enforcer:v1' uses the tag ':v1', which can be silently replaced by a malicious image at any time. It should be pinned to an immutable SHA digest, e.g. 'docker://ghcr.io/zkoppert/advanced-security-enforcer@sha256:<64-hex-char-digest>'.

Locations:

- `action.yml:8`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml from 'docker://ghcr.io/zkoppert/advanced-security-enforcer:v1' to 'docker://ghcr.io/zkoppert/advanced-security-enforcer@sha256:d7a0fc0a3a8732d80da177df5be460c4e4dc0e33d07c9ffaff23945c0a1cc6e7' # v1. The comment is placed outside the YAML single-quoted string to preserve readability while ensuring the image reference is immutable.

