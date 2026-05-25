# Standardize Console Logging for Operational Output and Diagnostics: Operational Scripts Test

These rules are ALWAYS ACTIVE for operational scripts, test utilities, and CLI tools in the `scripts/` directory and test infrastructure code that provides diagnostic output during development and CI/CD execution.

### Rules

- **R-CONSOLE-001** MUST: Operational scripts and test utilities MUST use console logging (console.log, console.error, console.warn) for outputting diagnostic information and execution status.
- **R-CONSOLE-002** MUST: Use console.error for all error conditions and failures to ensure proper stderr stream separation and CI/CD error detection.
- **R-CONSOLE-003** SHOULD: Prefix error messages with consistent markers (e.g., 'ERROR:', 'WARN:') to enable easier parsing and filtering.
- **R-CONSOLE-004** SHOULD: Consider adding optional --verbose or --debug flags for scripts that may benefit from additional diagnostic output.
- **R-CONSOLE-005** SHOULD: Ensure that exit codes align with console.error output (non-zero exit on errors).

### Verify

```bash
# Check for console logging statements in operational scripts and test utilities
grep -r "console\.log\|console\.error\|console\.warn" scripts/ packages/*/test*.ts --include="*.ts" | head -20

# Find all TypeScript files in scripts directory that use console
find scripts/ -name "*.ts" -exec grep -l "console\." {} \;

# Verify console.error usage in error paths
git grep "console\.error" -- "scripts/*.ts" "packages/*/test*.ts"
```

**Accept when:**
- Console logging statements are present in operational scripts and test utilities
- Error conditions use console.error for proper stderr output
- Scripts in the scripts/ directory and test utilities contain at least one console logging statement
- Error messages use consistent prefixes or formatting conventions
- Exit codes are non-zero when console.error is called for error conditions

<enforcement>
Claude Code MUST NOT skip or defer verification of console logging patterns in operational scripts and test utilities. All error paths MUST use console.error for proper stream separation.
</enforcement>