# Zod Schema Validation Adoption: Modules Not Bypass Schema Validation Coercing

These rules are ALWAYS ACTIVE for modules defining, validating, or evaluating structured data payloads across execution boundaries.

### Rules

- **R-ZOD-001** MUST_NOT: Modules MUST_NOT bypass schema validation by coercing unverified payloads directly into expected types.

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