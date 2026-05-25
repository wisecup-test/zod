# Standardize Console Logging for Operational Output and Diagnostics: Scripts Include Verbose

These rules are ALWAYS ACTIVE for all CLI scripts, operational utilities, test utilities, and build/validation tools in the `scripts/` directory and test infrastructure code that provides diagnostic output.

### Rules

- **R-CONSOLE-001** MUST: Use `console.error()` for all error conditions and failures to ensure proper stderr stream separation.
- **R-CONSOLE-002** MAY: Scripts MAY include verbose or debug logging modes that provide additional diagnostic output when enabled via command-line flags or environment variables.
- **R-CONSOLE-003** SHOULD: Prefix error messages with consistent markers (e.g., 'ERROR:', 'WARN:') to enable easier parsing and filtering.
- **R-CONSOLE-004** SHOULD: Ensure that exit codes align with `console.error()` output (non-zero exit on errors).
- **R-CONSOLE-005** SHOULD: Consider adding optional `--verbose` or `--debug` flags for scripts that may benefit from additional diagnostic output.

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
- Error conditions use `console.error()` for proper stderr output
- Scripts in the `scripts/` directory and test utilities contain at least one console logging statement
- Error messages use consistent prefixes (e.g., 'ERROR:', 'WARN:') where applicable
- Exit codes align with error output (non-zero on errors)

<enforcement>
Claude Code MUST NOT skip or defer verification of console logging patterns in scripts and test utilities. All error paths MUST use console.error() for proper stream separation. Violations require PR comments requesting appropriate console logging for diagnostic visibility.
</enforcement>