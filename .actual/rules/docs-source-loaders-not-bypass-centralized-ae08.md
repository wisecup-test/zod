# Fumadocs MDX Configuration Adoption: Source Loaders Not Bypass Centralized Configuration

These rules are ALWAYS ACTIVE for documentation subsystem modules defining content sources, schema collections, or MDX processing loaders.

### Rules

- **R-DOC-001** MUST_NOT: Source loaders MUST NOT bypass the centralized configuration schema when extracting structured documentation content.

### Verify

```bash
# Discover the workspace dependency manifest, locate the documentation validation script, and execute it using the project task runner.
# Locate the workspace typecheck script and run it to verify that all documentation source configurations and loaders conform to type definitions.
```

**Accept when:**
- Documentation source configurations compile without type errors.
- Content loader pipelines successfully parse and extract structured documentation text.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>