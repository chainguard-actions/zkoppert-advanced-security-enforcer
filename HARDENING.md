<!-- markdownlint-disable -->

# Hardening Report: zkoppert--advanced-security-enforcer/v1.0.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **zkoppert--advanced-security-enforcer/v1.0.3** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml uses a Docker image reference with a mutable tag instead of a SHA digest: `image: 'docker://ghcr.io/zkoppert/advanced-security-enforcer:v1'`. The tag `:v1` can be silently updated to point to a different (potentially malicious) image, creating a supply-chain risk. It should be pinned to a specific SHA digest, e.g. `image: 'docker://ghcr.io/zkoppert/advanced-security-enforcer@sha256:<64-hex-char-digest>'`.

Locations:

- `action.yml:7`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag `ghcr.io/zkoppert/advanced-security-enforcer:v1` with the immutable SHA digest `ghcr.io/zkoppert/advanced-security-enforcer@sha256:d7a0fc0a3a8732d80da177df5be460c4e4dc0e33d07c9ffaff23945c0a1cc6e7` in action.yml line 7. The original tag is preserved as a comment outside the YAML quotes for readability.

