# Lucide React Adoption for UI Iconography: Developers Apply Sizing Spacing Transition Styling

These rules are ALWAYS ACTIVE for documentation interface components requiring visual icons, interactive status glyphs, and documentation content loaders or metadata schemas defining navigation or section iconography.

### Rules

- **R-LUCIDE-001** SHOULD: Developers apply sizing, spacing, and transition styling to icon components through unified design system token class bindings rather than hardcoded inline style attributes.

### Verify

```bash
# Discover and run the project static analysis, type-checking, linting, and automated test suites
# Example project commands (verify actual repo configuration):
npm run lint
npm run typecheck
npm test
```

**Accept when:**
- All interface icon elements are imported directly from the adopted lucide-react library without unresolved module errors.
- Static analysis and lint checks pass cleanly with no prohibited inline vector elements or unapproved icon dependencies.
- Component test suites pass without accessibility warnings or rendering defects.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>