---
version: 2
name: cross-cutting-fs-promises-metadata-deserialization-han-7e5e
description: "node:fs/promises Metadata Deserialization: Handlers Not Allow Unhandled Deserialization Errors"
metadata:
  actual:
    adr_id: 7e5e4918-ddfc-4129-8ecf-c394134f5fd4
    status: accepted
    candidate_group_id: 11e6ee2f-8e4e-497b-bec8-a88de0f821d5
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/llms-full.txt/**
---

# node:fs/promises Metadata Deserialization: Handlers Not Allow Unhandled Deserialization Errors

Scope: applies to `packages/docs/app/llms-full.txt/**`.

These rules are ALWAYS ACTIVE for server route handlers and endpoint loaders performing asynchronous reads of local filesystem metadata, and internal metadata processing workflows using runtime filesystem modules.

### Rules

- **R-META-001** MUST_NOT: Handlers MUST_NOT allow unhandled deserialization errors from JSON.parse to crash the server response pipeline during endpoint execution.

### Verify

```bash
# Discover the project script runner and execute the automated test suite targeting route handlers and metadata loaders
# Discover the static analysis and linting command from the repository manifest and execute it against secure coding rules
# Inspect the build definition scripts and run the compilation check to confirm type safety across route handlers
npm test
npm run lint
npm run build
```

**Accept when:**
- Automated tests covering metadata retrieval and parsing pass without unhandled rejection or syntax errors.
- Static verification scripts report zero violations regarding unvalidated deserialization.
- Route execution successfully completes metadata ingestion and document ordering without throwing unhandled exceptions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated test execution, code reviews, and blocking pull requests omitting error boundaries or introducing synchronous filesystem calls.
</enforcement>