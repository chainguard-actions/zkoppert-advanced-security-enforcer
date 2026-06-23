<!-- markdownlint-disable -->

# Hardening Report: zkoppert--advanced-security-enforcer/v2.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **zkoppert--advanced-security-enforcer/v2.0.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml uses a Docker image reference with a mutable tag ('docker://ghcr.io/zkoppert/advanced-security-enforcer:v2') instead of an immutable SHA digest. This means the image could be silently replaced with a different (potentially malicious) version without any change to the action reference. It should be pinned to a specific SHA digest, e.g., 'docker://ghcr.io/zkoppert/advanced-security-enforcer@sha256:<64-hex-char-digest> # v2'.

Locations:

- `action.yml:8`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag 'docker://ghcr.io/zkoppert/advanced-security-enforcer:v2' with the immutable SHA digest 'docker://ghcr.io/zkoppert/advanced-security-enforcer@sha256:e6f11a95d12568a3183a5dbbaec6ca33930aa946a9f73af1086d47b47f641ae7' in action.yml line 8. The original tag 'v2' is preserved as a comment outside the YAML quotes for readability.

