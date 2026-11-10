---
version: 2
name: cross-cutting-fs-promises-metadata-deserialization-whe-2690
description: "node:fs/promises Metadata Deserialization: When Consuming Versioned Runtime Library Dependencies"
metadata:
  actual:
    adr_id: 2690918f-f47c-4e81-b216-cfc8b8201da3
    status: accepted
    candidate_group_id: 11e6ee2f-8e4e-497b-bec8-a88de0f821d5
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/llms-full.txt/**
---

# node:fs/promises Metadata Deserialization: When Consuming Versioned Runtime Library Dependencies

Scope: applies to `packages/docs/app/llms-full.txt/**`.

These rules are ALWAYS ACTIVE for server route handlers and internal metadata processing workflows using runtime filesystem modules.

### Rules

- **R-META-001** MUST: When consuming versioned runtime or library dependencies for parsing and file operations, developers MUST inspect the repository dependency manifest and lock artifact to resolve the exact version before implementation.
- **R-META-002** MUST: Isolate filesystem reads to asynchronous functions using `node:fs/promises` to avoid event loop stalls during route resolution.
- **R-META-003** MUST: Implement defensive error handling around `JSON.parse` invocations when deserializing local metadata files to gracefully handle unexpected file formats.

### Verify

```bash
# Discover and run the project script runner for automated tests targeting route handlers and metadata loaders
# Discover and run the static analysis / linting command against the repository
# Discover and run the build definition compilation check to confirm type safety across route handlers
```

**Accept when:**
- Automated tests covering metadata retrieval and parsing pass without unhandled rejection or syntax errors.
- Static verification scripts report zero violations regarding unvalidated deserialization.
- Route execution successfully completes metadata ingestion and document ordering without throwing unhandled exceptions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Pull requests omitting error boundaries or introducing synchronous filesystem calls must be blocked until remediated.
</enforcement>