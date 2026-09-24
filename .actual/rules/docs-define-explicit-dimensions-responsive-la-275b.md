# Adoption of next/image for Documentation Asset Rendering: Define Explicit Dimensions Responsive Layout Properties

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-DOC-001** MUST: Define explicit dimensions or responsive layout properties on all image component invocations to prevent layout shift.

### Verify

```bash
# Discover and run the repository linter to detect unoptimized image tag usage
# Discover and execute the repository type checker to validate image component properties
# Discover and execute the repository build script to confirm asset resolution and compilation integrity
```

**Accept when:**
- All image rendering in documentation presentation components passes automated lint and static analysis without unoptimized image violations
- Type verification succeeds across all component properties consuming the image module
- Repository build verification completes without missing asset or unresolved component errors

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>