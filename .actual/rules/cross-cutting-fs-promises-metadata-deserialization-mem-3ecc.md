---
version: 2
name: cross-cutting-fs-promises-metadata-deserialization-mem-3ecc
description: "node:fs/promises Metadata Deserialization: Memory Ordering Indices Derived Validated Metadata"
metadata:
  actual:
    adr_id: 3ecc633f-4898-4c61-98a2-9ae9e714cfe2
    status: accepted
    candidate_group_id: 11e6ee2f-8e4e-497b-bec8-a88de0f821d5
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/llms-full.txt/**
---

# node:fs/promises Metadata Deserialization: Memory Ordering Indices Derived Validated Metadata

Scope: applies to `packages/docs/app/llms-full.txt/**`.

These rules are ALWAYS ACTIVE for:
- Server route handlers and endpoint loaders performing asynchronous reads of local filesystem metadata.
- Internal metadata processing workflows using runtime filesystem modules.

### Rules

- **R-SCP-001** MAY: In-memory ordering indices MAY be derived from validated metadata entries to coordinate document sequencing.

### Verify

- Discover the project script runner and execute the automated test suite targeting route handlers and metadata loaders.
- Discover the static analysis and linting command from the repository manifest and execute it against secure coding rules.
- Inspect the build definition scripts and run the compilation check to confirm type safety across route handlers.

**Accept when:**

- Automated tests covering metadata retrieval and parsing pass without unhandled rejection or syntax errors.
- Static verification scripts report zero violations regarding unvalidated deserialization.
- Route execution successfully completes metadata ingestion and document ordering without throwing unhandled exceptions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated test execution verifying route handling and metadata parsing resilience.
- Verified by: Pull request code reviews ensuring proper error boundaries around asynchronous filesystem reads.
- Violation handling: Pull requests omitting error boundaries or introducing synchronous filesystem calls must be blocked until remediated.
- Exception process: Exceptions must be documented in code review and approved by the engineering lead when parsing non-JSON assets.
</enforcement>
