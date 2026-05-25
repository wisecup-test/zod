# Adopt Environment Variables for Runtime Configuration Sources: Sensitive Configuration Values

Status: proposed
Date: 2024-01-15
Deciders: Detection Pipeline (automated)

## Context

- The codebase requires runtime configuration that varies across deployment environments (development, staging, production)
- Configuration values such as API keys, service endpoints, and feature flags need to be externalized from source code
- Multiple components across the application (documentation generation, API routes, build scripts, data loaders) require access to environment-specific settings
- The pattern appears in 4 distinct files with 88.75% confidence, indicating consistent adoption across documentation, scripts, and loader modules
- Environment variables provide a standard mechanism for injecting configuration at runtime without code changes

## Problem Statement

Applications need a secure, flexible, and standardized way to manage configuration that varies across environments without hardcoding sensitive values or environment-specific settings into source code, while ensuring all components can access required configuration consistently.

## Decision

1. MUST: Sensitive configuration values (API keys, tokens, credentials) MUST NOT be hardcoded in source files

## Policy Block

- MUST Sensitive configuration values (API keys, tokens, credentials) MUST NOT be hardcoded in source files

In scope:
- All runtime configuration that varies by deployment environment
- API keys, authentication tokens, and service credentials
- External service endpoints and URLs
- Feature flags and behavioral toggles
- Build-time and runtime scripts requiring environment-specific values

Out of scope:
- Static configuration that never changes across environments
- Type definitions and interface declarations
- Algorithm constants and mathematical values
- UI text and localization strings (unless environment-specific)

Exceptions:
- EXC-001: Development-only configuration for local testing where security is not a concern

## Rationale

- Pattern detected across 4 files with 88.75% confidence indicates established practice in the codebase for configuration management
- Environment variables align with 12-factor app methodology and are supported natively in Node.js and modern deployment platforms
- Separating configuration from code enables the same codebase to run in multiple environments without modification
- Using process.env provides a secure mechanism to inject secrets without exposing them in version control

## Consequences

Positive:
- Configuration can be changed without code modifications or redeployment
- Sensitive credentials are kept out of version control and source code
- Same codebase can be deployed to multiple environments with different configurations
- Aligns with industry best practices and cloud-native deployment patterns
- Simplifies CI/CD pipelines by allowing environment-specific injection

Negative:
- Environment variables must be managed and documented separately from code
- Missing or misconfigured environment variables can cause runtime failures
- Debugging configuration issues may require access to deployment environment
- Type safety is reduced as environment variables are always strings requiring parsing

## Alternatives

- Hardcode configuration values directly in source files (rejected)
  Rejected because: Exposes sensitive credentials in version control, requires code changes for environment-specific values, violates security best practices
  When valid: Never valid for production systems with sensitive data
- Use configuration files (JSON/YAML) checked into version control (rejected)
  Rejected because: Still exposes sensitive values in version control, requires separate files per environment, less flexible than environment variables
  When valid: Acceptable for non-sensitive static configuration that rarely changes
- Use external configuration services (AWS Parameter Store, HashiCorp Vault) (deferred)
  Rejected because: Adds infrastructure complexity and dependencies, may be overkill for current needs
  When valid: Consider for large-scale deployments requiring centralized secret management and rotation

## Risks

- Missing environment variables cause runtime failures in production
  Mitigation: Implement startup validation that checks for required environment variables and fails fast with clear error messages
  Owner: Engineering team
- Environment variables are accidentally logged or exposed in error messages
  Mitigation: Implement logging filters to redact sensitive values, use structured logging with explicit field control
  Owner: Engineering team
- Inconsistent environment variable naming leads to confusion and errors
  Mitigation: Document all environment variables in README or .env.example file, establish naming conventions
  Owner: Engineering team

## Implementation Notes

- Create a .env.example file documenting all required and optional environment variables with descriptions
- Use a library like dotenv for local development to load variables from .env files (never commit actual .env files)
- Consider creating a configuration module that validates and exports typed configuration objects at startup
- Document environment variables in deployment guides and ensure they are set in all deployment environments

## Continuation Context


Verify commands:
- grep -r 'process\.env\.' --include='*.ts' --include='*.tsx' --include='*.js' | head -20
- grep -r 'API_KEY\|TOKEN\|SECRET' --include='*.ts' --include='*.tsx' | grep -v 'process.env' | grep -v '.env.example'
- test -f .env.example && echo 'Environment template exists' || echo 'Missing .env.example'

Accept when:
- All environment-specific configuration values are accessed via process.env
- No hardcoded API keys, tokens, or credentials found in source files
- A .env.example file exists documenting all required environment variables

## Enforcement

- Verified by: Automated grep-based checks in CI pipeline scanning for hardcoded credentials
- Verified by: Code review checklist includes verification that new configuration uses environment variables
- Verified by: Static analysis tools configured to flag suspicious hardcoded values
- Violation handling: CI pipeline fails if hardcoded credentials are detected in source files
- Violation handling: Code review blocks merge if configuration is not properly externalized
- Violation handling: Security team notified for review if sensitive values are found in commits
- Exception process: Request exception via tech lead with justification for why environment variables cannot be used
- Exception process: Document exception in code comments with EXC-001 reference and approval date
- Exception process: Review exceptions quarterly to determine if they can be eliminated