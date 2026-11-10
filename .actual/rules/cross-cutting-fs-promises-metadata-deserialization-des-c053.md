---
version: 2
name: cross-cutting-fs-promises-metadata-deserialization-des-c053
description: "node:fs/promises Metadata Deserialization: Deserialization Filesystem Contents Retrieved Via Readfile"
metadata:
  actual:
    adr_id: c0532532-08f4-4cd2-9107-14951abbb0fa
    status: accepted
    candidate_group_id: 11e6ee2f-8e4e-497b-bec8-a88de0f821d5
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/llms-full.txt/**
---

# node:fs/promises Metadata Deserialization: Deserialization Filesystem Contents Retrieved Via Readfile

Scope: applies to `packages/docs/app/llms-full.txt/**`.

These rules are ALWAYS ACTIVE for server route handlers and endpoint loaders performing asynchronous reads of local filesystem metadata, and internal metadata processing workflows using runtime filesystem modules.

### Rules

- **R-META-001** SHOULD: Deserialization of filesystem contents retrieved via fs.readFile SHOULD implement defensive runtime schema validation rather than relying solely on direct JSON.parse invocations.
- **R-META-002** MANDATORY: Isolate filesystem reads to asynchronous functions to avoid event loop stalls during route resolution.
- **R-META-003** MANDATORY: Implement defensive error handling around JSON.parse invocations to gracefully handle unexpected file formats.

### Verify

```bash
# Discover and execute the automated test suite targeting route handlers and metadata loaders
# Discover the static analysis and linting command from the repository manifest and execute it
# Inspect the build definition scripts and run the compilation check to confirm type safety across route handlers
```

**Accept when:**
- Automated tests covering metadata retrieval and parsing pass without unhandled rejection or syntax errors.
- Static verification scripts report zero violations regarding unvalidated deserialization.
- Route execution successfully completes metadata ingestion and document ordering without throwing unhandled exceptions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Pull requests omitting error boundaries or introducing synchronous filesystem calls must be blocked until remediated.
</enforcement>