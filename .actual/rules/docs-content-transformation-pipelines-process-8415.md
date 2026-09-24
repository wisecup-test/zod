# Fumadocs MDX Configuration Adoption: Content Transformation Pipelines Process Document Nodes

These rules are ALWAYS ACTIVE for documentation subsystem modules defining content sources, schema collections, or MDX processing loaders.

### Rules

- **R-DOC-001** MUST: Content transformation pipelines MUST process document nodes through ordered remark middleware chains compatible with the configured MDX source pipeline.

### Verify

```bash
# Discover workspace dependency manifest, locate documentation validation script, and execute via task runner
# Locate workspace typecheck script and run to verify source configurations and loaders conform to type definitions
```

**Accept when:**
- Documentation source configurations compile without type errors.
- Content loader pipelines successfully parse and extract structured documentation text.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>