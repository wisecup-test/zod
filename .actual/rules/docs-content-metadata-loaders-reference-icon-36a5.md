# Lucide React Adoption for UI Iconography: Content Metadata Loaders Reference Icon Component

These rules are ALWAYS ACTIVE for documentation interface components requiring visual icons or interactive status glyphs, and documentation content loaders and metadata schemas defining navigation or section iconography.

### Rules

- **R-LUCIDE-001** MAY: Content metadata loaders MAY reference icon component symbols from lucide-react to associate navigational tree entries with consistent visual indicators.
- **R-LUCIDE-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-LUCIDE-003** MANDATORY: Before writing code that uses a versioned library, execute in order: find the dependency manifest, identify the build tool, inspect the repository lock artifact for the exact resolved version, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-run steps per dependency at point of use.
- **R-LUCIDE-004** MANDATORY: Locate the project dependency declaration to verify the presence of lucide-react and inspect the repository lock artifact to confirm the active locked version prior to adding new icon references.
- **R-LUCIDE-005** MANDATORY: Apply consistent size utility classes to icon component instances to maintain alignment with typography and surrounding interactive elements.

### Verify

```bash
# Discover and run the project static analysis and type-checking scripts
# Discover and run the project linting and validation suites
# Discover and run the project automated test suites
```

**Accept when:**
- All interface icon elements are imported directly from the adopted lucide-react library without unresolved module errors.
- Static analysis and lint checks pass cleanly with no prohibited inline vector elements or unapproved icon dependencies.
- Component test suites pass without accessibility warnings or rendering defects.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration pipeline executing static analysis, type checking, and linting rules, and peer code review.
</enforcement>