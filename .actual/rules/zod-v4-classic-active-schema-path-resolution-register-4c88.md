# Zod Contextual Reference Cache and Circular Reference Tracking Pattern: Active Schema Path Resolution Register Target

These rules are ALWAYS ACTIVE for all schema translation and conversion routines dealing with external structural schema specifications.

### Rules

- **R-ZOD-001** MUST: Active schema path resolution MUST register the target path in ctx.processing and MUST invoke ctx.processing.delete upon completion to release cycle tracking state.
- **R-ZOD-002** MANDATORY: Wrap reference compilation within structured resource release blocks ensuring cleanup of processing tracking entries.
- **R-ZOD-003** MANDATORY: Scope context instances strictly to individual translation invocations or partition cache namespaces by document root to avoid cache collisions.
- **R-ZOD-004** MANDATORY: Follow LOCK-VERSION GROUNDING before writing code that uses a versioned library: find dependency manifest, identify build tool, inspect lock/resolution artifact for exact version, look up official documentation for that exact version, and confirm every API exists.

### Verify

```bash
# Discover and run the project test runner to verify recursive schema reference tests pass without stack overflow
# Execute project static analysis and linting suites to ensure context parameters are consistently passed
```

**Accept when:**
- All unit tests covering circular and self-referencing schema compilation complete successfully without recursion errors.
- Static type analysis confirms all schema conversion functions conform to expected context signatures.

<enforcement>
Claude Code MUST NOT skip or defer verification. Pull requests omitting reference cache checks or cycle tracking cleanup in schema translation modules will be blocked during review, and static verification failures on context interface mismatches halt compilation.
</enforcement>