# Zod Schema Validation Adoption: Data Structures Processed Across External Untrusted

These rules are ALWAYS ACTIVE for modules defining, validating, or evaluating structured data payloads across execution boundaries, and components processing external or unverified input structures.

### Rules

- **R-ZOD-001** MUST: Data structures processed across external or untrusted boundaries MUST be defined using zod schemas.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute validation
# Discover the project type check configuration and execute static analysis
```

**Accept when:**
- All data structures entering validation boundaries conform to defined zod schemas and pass schema parse calls without error.
- Repository verification scripts execute successfully with zero validation or type checking errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>