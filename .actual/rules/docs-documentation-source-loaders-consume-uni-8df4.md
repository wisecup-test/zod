# Fumadocs MDX Configuration Adoption: Documentation Source Loaders Consume Unified Definitions

These rules are ALWAYS ACTIVE for all documentation subsystem modules defining content sources, schema collections, or MDX processing loaders.

### Rules

- **R-DOC-001** MUST: Documentation source loaders MUST consume unified source definitions established through the centralized configuration module rather than declaring independent file-system schemas.

### Verify

```bash
# Discover the workspace dependency manifest, locate the documentation validation script, and execute it using the project task runner.
# Locate the workspace typecheck script and run it to verify that all documentation source configurations and loaders conform to type definitions.
```

**Accept when:**
- Documentation source configurations compile without type errors.
- Content loader pipelines successfully parse and extract structured documentation text.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via continuous integration automated typecheck and build validation pipelines and peer code review.
</enforcement>