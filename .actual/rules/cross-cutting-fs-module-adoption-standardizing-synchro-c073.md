---
version: 2
name: cross-cutting-fs-module-adoption-standardizing-synchro-c073
description: "node:fs Module Adoption: Standardizing Synchronous File System Access in Repository Automation Scripts: Before Introducing Updating Any External Dependency"
metadata:
  actual:
    adr_id: c0732987-dab1-4589-ba17-2d85a2067e5c
    status: accepted
    candidate_group_id: f60af43a-94a4-4f74-b47b-742a1e4db0fd
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - .claude/skills/triage/scripts/**
      - scripts/**
---

# node:fs Module Adoption: Standardizing Synchronous File System Access in Repository Automation Scripts: Before Introducing Updating Any External Dependency

Scope: applies to `.claude/skills/triage/scripts/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for:
- Standalone repository maintenance, triage, verification, and code generation scripts.
- Local file system inspection and artifact writing workflows executed outside of published distribution packages.

### Rules

- **R-LM-001** MUST: Before introducing or updating any external dependency associated with repository tooling, engineers MUST inspect the project dependency manifest and lock artifact to resolve the exact locked version.

### Verify

- Discover the project verification script defined in the repository configuration manifest and execute it to verify repository integrity.
- Inspect script source files to confirm all file system imports utilize the protocol-prefixed core module namespace without third-party wrapper dependencies.

**Accept when:**

- All repository automation and verification scripts execute to completion without file system resolution errors.
- Static module import analysis confirms file system access in script files is restricted to the protocol-qualified core module namespace.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration checks that execute verification scripts on every pull request.
- Verified by: Static analysis and peer review of newly introduced or modified script files.
- Violation handling: Pull requests introducing third-party file system utilities or non-protocol-qualified imports in scripts will be blocked during review until updated to adhere to core module standards.
- Exception process: Exceptions require documented justification and approval from engineering leads where specialized third-party file manipulation features are demonstrably necessary.
</enforcement>
