---
version: 2
name: cross-cutting-fs-promises-metadata-deserialization-app-7b60
description: "node:fs/promises Metadata Deserialization: Application Encapsulate Asynchronous Filesystem Operations Node"
metadata:
  actual:
    adr_id: 7b60d2b7-c1b1-4714-8256-774134d9270e
    status: accepted
    candidate_group_id: 11e6ee2f-8e4e-497b-bec8-a88de0f821d5
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/llms-full.txt/**
---

# node:fs/promises Metadata Deserialization: Application Encapsulate Asynchronous Filesystem Operations Node

Scope: applies to `packages/docs/app/llms-full.txt/**`.

These rules are ALWAYS ACTIVE for server route handlers, endpoint loaders, and internal metadata processing workflows performing asynchronous reads of local filesystem metadata.

### Rules

- **R-FS-001** MUST: The application MUST encapsulate asynchronous filesystem operations using the node:fs/promises module when retrieving local documentation metadata.

### Verify

```bash
# Discover the project script runner and execute the automated test suite targeting route handlers and metadata loaders.
# Discover the static analysis and linting command from the repository manifest and execute it against secure coding rules.
# Inspect the build definition scripts and run the compilation check to confirm type safety across route handlers.
```

**Accept when:**
- Automated tests covering metadata retrieval and parsing pass without unhandled rejection or syntax errors.
- Static verification scripts report zero violations regarding unvalidated deserialization.
- Route execution successfully completes metadata ingestion and document ordering without throwing unhandled exceptions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>