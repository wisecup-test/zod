# Standardize Console Logging for Operational Output and Diagnostics: Error Conditions Failures

These rules are ALWAYS ACTIVE for CLI scripts, operational utilities, test utilities, and test infrastructure code that provides diagnostic output in the scripts/ directory and test files.

### Rules

- **R-CONSOLE-001** MUST: Error conditions and failures MUST be logged to console.error to enable proper stream separation and error detection in CI/CD pipelines.

### Verify

```bash
# Check for console logging statements in operational scripts and test utilities
grep -r "console\.log\|console\.error\|console\.warn" scripts/ packages/*/test*.ts --include="*.ts" | head -20

# Find all TypeScript files in scripts directory that use console
find scripts/ -name "*.ts" -exec grep -l "console\." {} \;

# Verify console.error usage for error paths
git grep "console\.error" -- "scripts/*.ts" "packages/*/test*.ts"
```

**Accept when:**
- Console logging statements are present in operational scripts and test utilities
- Error conditions use console.error for proper stderr output
- Scripts in the scripts/ directory and test utilities contain at least one console logging statement
- Error paths consistently route to console.error rather than console.log

<enforcement>
Claude Code MUST NOT skip or defer verification of console.error usage in error paths. All error conditions in operational scripts and test utilities must be verified to use console.error for proper CI/CD stream separation.
</enforcement>