---
version: 2
name: cross-cutting-engineers-discover-ecosystem-lock-artifa-84c3
description: "Direct process.env Runtime Configuration Access in Automation Scripts: Engineers Discover Ecosystem Lock Artifact Confirm"
metadata:
  actual:
    adr_id: 84c3922c-9359-452a-a457-3c46b8e8abe9
    status: accepted
    candidate_group_id: 2cca4728-a9b2-4bc1-8b4e-e02788c4b31b
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Direct process.env Runtime Configuration Access in Automation Scripts: Engineers Discover Ecosystem Lock Artifact Confirm

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for:
- Repository automation, validation, and maintenance scripts reading execution parameters and pipeline signaling variables.

### Rules

- **R-SC-001** MUST: Engineers MUST discover the ecosystem lock artifact and confirm all dependency versions prior to introducing external environment parsing libraries.

### Verify

- Discover and run the project repository script verification and type-checking suites across automation scripts.
- Execute the repository linting and static analysis suite to check for unvalidated environment variable references.

**Accept when:**

- All automation and maintenance scripts execute cleanly without unhandled undefined environment variable exceptions.
- Static analysis and type checking pass across all repository automation scripts without unhandled configuration types.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration pipeline execution across pull requests.
- Verified by: Peer code review verification of script modifications and environment variable usage.
- Violation handling: Pull requests introducing unvalidated or sensitive credential handling via plain environment variables are blocked until remediated.
- Exception process: Exceptions require documented review and architectural sign-off justifying why direct environment access is insufficient or why dedicated secret retrieval is needed.
</enforcement>
