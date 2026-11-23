---
version: 2
name: cross-cutting-fs-module-adoption-standardizing-synchro-0857
description: "node:fs Module Adoption: Standardizing Synchronous File System Access in Repository Automation Scripts: Repository Automation Code Generation Verification Scripts"
metadata:
  actual:
    adr_id: 08574c33-4cc0-4dc0-a9cd-1bb01863f83d
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

# node:fs Module Adoption: Standardizing Synchronous File System Access in Repository Automation Scripts: Repository Automation Code Generation Verification Scripts

Scope: applies to `.claude/skills/triage/scripts/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for:
- Standalone repository maintenance, triage, verification, and code generation scripts.
- Local file system inspection and artifact writing workflows executed outside of published distribution packages.

### Rules

- **R-LM-001** MUST: Repository automation, code generation, and verification scripts MUST import file system capabilities exclusively from the core node:fs module using explicit protocol-qualified specifiers.

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
