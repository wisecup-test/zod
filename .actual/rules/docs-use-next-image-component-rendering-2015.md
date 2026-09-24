# Adoption of next/image for Documentation Asset Rendering: Use Next Image Component Rendering Raster

These rules are ALWAYS ACTIVE for all documentation presentation components, layout structures, and raster image assets matching the configured scope.

### Rules

- **R-DOC-001** MUST: Use the next/image component for rendering raster image assets, logos, and illustrations across documentation presentation components and layout structures.
- **R-DOC-002** MANDATORY (DISCOVERY POLICY): Omit all tool names, file names, commands, package managers, and version numbers in ADRs, deriving them from the project repository.
- **R-DOC-003** MANDATORY (LOCK-VERSION GROUNDING): Before writing code using a versioned library, find the dependency manifest, identify the build tool, inspect the repository lock/resolution artifact for the exact version, look up official documentation for that version, and confirm every API exists in that exact version.

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