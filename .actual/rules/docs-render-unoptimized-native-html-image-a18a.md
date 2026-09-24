# Adoption of next/image for Documentation Asset Rendering: Render Unoptimized Native Html Image Elements

These rules are ALWAYS ACTIVE for documentation UI components and layouts rendering visual assets.

### Rules

- **R-DOC-001** MUST_NOT: Render unoptimized native HTML image elements for documentation assets where the standardized image component is applicable.

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
Claude Code MUST NOT skip or defer verification. All image rendering must use the standardized framework image module.
</enforcement>