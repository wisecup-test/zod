# Fumadocs MDX Configuration Adoption: Before Implementing Updating Any Dependency Integration

These rules are ALWAYS ACTIVE for documentation subsystem modules defining content sources, schema collections, or MDX processing loaders.

### Rules

- **R-FUM-001** MUST: Before implementing or updating any dependency integration, inspect the repository lock or resolution artifact to determine and adhere to the exact resolved dependency version.
- **R-FUM-002** MUST: Discover the workspace dependency manifest to locate documentation configuration entry points before adding new content collections.
- **R-FUM-003** MUST: Ensure that custom markdown and remark transformation plugins integrate directly with the source loader processing chain.

### Verify

```bash
# Discover workspace dependency manifest, locate the documentation validation script, and execute it using the project task runner
# Locate the workspace typecheck script and run it to verify documentation source configurations and loaders conform to type definitions
```

**Accept when:**
- Documentation source configurations compile without type errors.
- Content loader pipelines successfully parse and extract structured documentation text.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>