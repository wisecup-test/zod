# Standardize Console Logging for Operational Output and Diagnostics: Scripts Log Progress

Status: proposed
Date: 2024-01-09
Deciders: Detection Pipeline (automated)

## Context

- The codebase contains multiple scripts and test utilities that require operational visibility during execution, including version checking, semver validation, and package resolution testing
- Console logging provides immediate feedback for CLI tools and scripts that are executed in development and CI/CD environments where structured logging frameworks may be excessive
- Pattern detected across 4 files with 92.07% confidence, indicating a consistent approach to logging in operational tooling and test infrastructure
- Scripts need to communicate progress, errors, and diagnostic information to operators and developers in real-time without requiring complex logging infrastructure

## Problem Statement

Scripts, test utilities, and operational tools require a consistent approach to outputting diagnostic information, progress updates, and error messages. Without standardized logging practices, these tools may produce inconsistent output formats, making it difficult for developers and CI systems to parse results, diagnose issues, and understand execution flow.

## Decision

1. SHOULD: Scripts SHOULD log progress indicators and status updates to console.log to provide visibility into long-running operations

## Policy Block

- SHOULD Scripts SHOULD log progress indicators and status updates to console.log to provide visibility into long-running operations

In scope:
- CLI scripts and operational utilities in the scripts/ directory
- Test utilities and test infrastructure code that provides diagnostic output
- Build and validation tools that execute in CI/CD environments
- Development tools that require real-time feedback to developers

Out of scope:
- Production application code running in server environments
- Library code that should not produce side effects
- Code that requires structured logging with log levels, metadata, and aggregation
- Long-running services that need log rotation and management

Exceptions:
- EXC-001: A script requires structured JSON output for machine parsing
- EXC-002: Silent execution is required for scripts used in pipelines where output is captured

## Rationale

- Console logging is the simplest and most appropriate mechanism for scripts and utilities that execute in terminal environments, providing immediate feedback without additional dependencies
- The pattern appears consistently across operational tooling (check-semver.ts, check-versions.ts) and test infrastructure (attw.test.ts, test-resolution.ts), indicating an established practice
- Stream separation (stdout vs stderr) enables CI/CD systems to detect failures and parse output effectively
- Console logging aligns with the ephemeral nature of script execution where logs do not need persistence or aggregation

## Consequences

Positive:
- Consistent diagnostic output across all operational scripts and test utilities
- Simplified debugging and troubleshooting through visible execution flow
- Proper error detection in CI/CD pipelines through stderr stream separation
- Zero additional dependencies or infrastructure required for basic operational visibility

Negative:
- Console output cannot be easily filtered by log level without custom parsing
- No built-in support for structured logging or metadata attachment
- Output may become noisy in scripts that perform many operations
- Difficult to redirect or suppress output selectively without modifying code

## Alternatives

- Adopt a structured logging library (e.g., winston, pino) for all scripts (rejected)
  Rejected because: Adds unnecessary complexity and dependencies for simple scripts that execute briefly in terminal environments. Structured logging is better suited for long-running services.
  When valid: Consider for complex scripts that require log level filtering, metadata attachment, or integration with log aggregation systems
- Use a custom logging utility wrapper that provides consistent formatting (deferred)
  Rejected because: Not rejected, but deferred pending evaluation of whether formatting consistency becomes a pain point
  When valid: Implement if scripts grow to require consistent timestamp formatting, color coding, or prefix conventions
- Suppress all logging and rely solely on exit codes (rejected)
  Rejected because: Eliminates visibility into script execution, making debugging and troubleshooting significantly more difficult for developers
  When valid: Only appropriate for scripts explicitly designed for silent pipeline integration with --quiet flags

## Risks

- Excessive console output may obscure important error messages in verbose scripts
  Mitigation: Implement consistent conventions for error formatting (e.g., prefixing with 'ERROR:') and ensure errors always use console.error
  Owner: Engineering team
- Scripts may produce inconsistent output formats making automated parsing difficult
  Mitigation: Document output format conventions and consider providing machine-readable output modes (JSON) for scripts used in automation
  Owner: DevOps team
- Console logging in test utilities may interfere with test framework output
  Mitigation: Use test framework logging mechanisms where available, or ensure console output is clearly distinguished from test results
  Owner: Engineering team

## Implementation Notes

- Use console.error for all error conditions and failures to ensure proper stream separation
- Consider adding optional --verbose or --debug flags for scripts that may benefit from additional diagnostic output
- Prefix error messages with consistent markers (e.g., 'ERROR:', 'WARN:') to enable easier parsing and filtering
- For scripts used in CI/CD, ensure that exit codes align with console.error output (non-zero exit on errors)

## Continuation Context


Verify commands:
- grep -r "console\.log\|console\.error\|console\.warn" scripts/ packages/*/test*.ts --include="*.ts" | head -20
- find scripts/ -name "*.ts" -exec grep -l "console\." {} \;
- git grep "console\.error" -- "scripts/*.ts" "packages/*/test*.ts"

Accept when:
- Console logging statements are present in operational scripts and test utilities
- Error conditions use console.error for proper stderr output
- Scripts in the scripts/ directory and test utilities contain at least one console logging statement

## Enforcement

- Verified by: Code review for new scripts and test utilities
- Verified by: Automated grep-based checks in CI to verify console.error usage for error paths
- Verified by: Manual inspection during PR review to ensure appropriate logging levels
- Violation handling: PR comments requesting addition of appropriate console logging for diagnostic visibility
- Violation handling: Rejection of scripts that fail silently without error output
- Violation handling: Guidance provided to use console.error for error conditions
- Exception process: Request exception during PR review with justification for alternative approach
- Exception process: Team lead approval required for scripts that require structured output or silent execution
- Exception process: Document exception rationale in script header comments or README