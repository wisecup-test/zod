# Lucide React Adoption for UI Iconography: Developers Not Embed Raw Inline Scalable

These rules are ALWAYS ACTIVE for all documentation interface components, content loaders, and metadata schemas requiring visual icons or interactive status glyphs.

### Rules

- **R-LUCIDE-001** MUST_NOT: Developers MUST_NOT embed raw inline scalable vector graphic markup or introduce alternative third-party icon packages for interface glyphs within the documentation subsystem.

### Verify

```bash
# Discover and run static analysis, type-checking, linting, and test suites to verify icon imports and catch prohibited inline vectors or unapproved packages.
# (Note: Specific tool names and commands must be derived from the repository manifest and configuration files)
```

**Accept when:**
- All interface icon elements are imported directly from the adopted lucide-react library without unresolved module errors.
- Static analysis and lint checks pass cleanly with no prohibited inline vector elements or unapproved icon dependencies.
- Component test suites pass without accessibility warnings or rendering defects.

<enforcement>
Claude Code MUST NOT skip or defer verification. Pull requests introducing raw inline vector markup or unapproved icon dependencies will fail automated checks and require remediation before merge.
</enforcement>