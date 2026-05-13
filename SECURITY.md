Repo: gateway

# Security Policy

This document describes how to report security vulnerabilities to the iAiFy
enterprise and what security guarantees we provide for this repository.

## Reporting a Vulnerability

If you believe you have found a security vulnerability in this repository,
please report it privately. Do **not** open a public GitHub issue.

- **Email:** ashkan.soleimani.m@gmail.com
- **GitHub Security Advisories:** use the *Security* tab on this repository
  and click *Report a vulnerability* to open a private advisory.

We commit to:

- Acknowledging your report within **5 business days**.
- Providing a triage assessment within **15 business days**.
- Coordinating a fix and public disclosure within **90 days** of the initial
  report. We may extend this window for severe vulnerabilities that require
  upstream coordination; in such cases we will inform the reporter.

When reporting, please include:

- A clear description of the issue and the affected component or version.
- Reproduction steps and, where possible, a minimal proof of concept.
- An impact assessment (what an attacker can achieve).

## Supported Versions

In keeping with our GHCR image retention policy (keep-2), we provide
security fixes for the **two most recent minor releases** of this project.

| Version           | Supported          |
| ----------------- | ------------------ |
| Latest minor      | Yes                |
| Previous minor    | Yes (security only)|
| Older versions    | No                 |

End-of-life versions will not receive security patches. Users on unsupported
versions are encouraged to upgrade.

## Security Measures

This repository inherits the following baseline controls from the
iAiFy enterprise standard:

- **Signed commits.** All maintainer commits are signed with `ed25519` SSH
  keys; unsigned commits to protected branches are rejected by CI.
- **Container provenance.** Published container images are signed with
  [cosign](https://docs.sigstore.dev/cosign/overview/) and shipped with a
  CycloneDX SBOM as an OCI attachment.
- **Secret management.** Application secrets are sourced through the
  enterprise chain: Doppler -> Infisical -> HashiCorp Vault. Secrets are
  never committed to the repository, and `.env*` files are gitignored.
- **Branch protection.** The default branch requires at least **1 approving
  PR review**, status-check passage, and disallows force-pushes and direct
  pushes.
- **Dependency hygiene.** Dependabot is enabled for ecosystem manifests, and
  CodeQL runs on every pull request to the default branch.

## PGP / SSH Signing Key Fingerprint

```
<TO_BE_FILLED>
```

The signing key used to verify release artifacts and tag signatures will be
published here once rotated under the enterprise key-management process.

---

For enterprise-wide security policy and governance, see
[Ai-road-4-You/governance](https://github.com/Ai-road-4-You/governance).
