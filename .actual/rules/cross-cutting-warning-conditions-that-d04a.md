# Standardize Console Logging for Operational Output and Diagnostics: Warning Conditions That

These rules are ALWAYS ACTIVE for all CLI scripts, operational utilities, test infrastructure code, build and validation tools, and development tools that require real-time feedback to developers.

### Rules

- **R-CONSOLE-001** SHOULD: Warning conditions that do not halt execution SHOULD be logged to console.warn to distinguish them from errors and informational messages.
- **R-CONSOLE-002** MUST: Use console.error for all error conditions and failures to ensure proper stream separation to stderr.
- **R-CONSOLE-003** SHOULD: Prefix error messages with consistent markers (e.g., 'ERROR:', 'WARN:') to enable easier parsing and filtering.
- **R-CONSOLE-004** SHOULD: Consider adding optional --verbose or --debug flags for scripts that may benefit from additional diagnostic output.
- **R-CONSOLE-005** MUST: For scripts used in CI/CD, ensure that exit codes align with console.error output (non-zero exit on errors).

### Verify

```bash
# Check for console logging statements in operational scripts and test utilities
grep -r "console\.log\|console\.error\|console\.warn" scripts/ packages/*/test*.ts --include="*.ts" | head -20

# Find all TypeScript files in scripts directory that use console methods
find scripts/ -name "*.ts" -exec grep -l "console\." {} \;

# Verify console.error usage for error paths
git grep "console\.error" -- "scripts/*.ts" "packages/*/test*.ts"
```

**Accept when:**
- Console logging statements are present in operational scripts and test utilities
- Error conditions use console.error for proper stderr output
- Scripts in the scripts/ directory and test utilities contain at least one console logging statement
- Warning conditions use console.warn instead of console.log or console.error
- Error messages include consistent prefixes for automated parsing

<enforcement>
Claude Code MUST NOT skip or defer verification. All console logging in operational scripts and test utilities MUST comply with these rules during code review and automated CI checks.
</enforcement>