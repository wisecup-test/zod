# Fumadocs MDX Configuration Adoption: Documentation Content Sources Loader Pipelines Define

These rules are ALWAYS ACTIVE for documentation subsystem modules defining content sources, schema collections, or MDX processing loaders.

### Rules

- **R-DOC-001** MUST: Documentation content sources and loader pipelines MUST define and consume their content configuration using the fumadocs-mdx/config module.

### Verify

```bash
# Discover workspace dependency manifest, locate documentation validation script, and execute via project task runner
# Locate workspace typecheck script and run to verify documentation source configurations and loaders conform to type definitions
```

**Accept when:**
- Documentation source configurations compile without type errors.
- Content loader pipelines successfully parse and extract structured documentation text.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>