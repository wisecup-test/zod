# Zod Schema Validation Adoption: Schemas Composite Data Structures Constructed Object

These rules are ALWAYS ACTIVE for modules defining, validating, or evaluating structured data payloads across execution boundaries, and components processing external or unverified input structures.

### Rules

- **R-ZOD-001** MUST: Schemas for composite data structures MUST be constructed using z.object with explicit field property schemas.

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