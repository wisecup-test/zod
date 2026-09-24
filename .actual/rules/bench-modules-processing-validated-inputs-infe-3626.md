# Zod Schema Validation Adoption: Modules Processing Validated Inputs Infer Internal

These rules are ALWAYS ACTIVE for modules defining, validating, or evaluating structured data payloads across execution boundaries, and components processing external or unverified input structures.

### Rules

- **R-ZOD-001** SHOULD: Modules processing validated inputs infer internal types directly from zod schemas rather than maintaining duplicate type declarations.
- **R-ZOD-002** MANDATORY: The consumer MUST derive tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-ZOD-003** MANDATORY: Before writing code that uses a versioned library, the consumer MUST follow the LOCK-VERSION GROUNDING sequence: find dependency manifest, identify build tool, inspect lock/resolution artifact, look up official documentation for exact version, confirm every API/class/function exists, and re-run per dependency at point of use.
- **R-ZOD-004** MANDATORY: Declare reusable schemas for domain models using `z.object` and composite schema primitives.
- **R-ZOD-005** MANDATORY: Invoke the parse method at boundary entry points to fail fast on invalid input structures before proceeding with domain logic.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute validation
# Discover the project type check configuration and execute static analysis
```

**Accept when:**
- All data structures entering validation boundaries conform to defined zod schemas and pass schema parse calls without error.
- Repository verification scripts execute successfully with zero validation or type checking errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration test suites, static analysis checks, and peer code reviews verifying that untrusted inputs pass through schema parse methods.
</enforcement>