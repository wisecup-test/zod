# Adopt Structured Error Message Localization for Public API Validation: Error Handling Implementations

Status: proposed
Date: 2024-01-15
Deciders: Detection Pipeline (automated)

## Context

- The codebase contains a validation library (Zod) that exposes public APIs for schema validation with extensive internationalization support across multiple locales (ko, pl, kh, mk, etc.)
- Error messages and validation feedback are critical components of the public API contract, requiring consistent structure and localization capabilities
- The pattern appears across 33 files with 90.45% confidence, indicating a systematic approach to error handling and message formatting in public-facing validation APIs
- Multiple versions (v3, v4) and variants (classic, mini) suggest an evolving API design with backward compatibility requirements
- Benchmark files indicate performance considerations are important for this validation library's public API design

## Problem Statement

Public validation APIs must provide clear, actionable error messages to external consumers in multiple languages and formats, while maintaining consistent structure, performance, and backward compatibility across API versions. Without standardized localization and error message contracts, API consumers face inconsistent error handling experiences and integration challenges.

## Decision

1. SHOULD: Error handling implementations SHOULD support both classic and minimal variants to accommodate different performance and bundle size requirements

## Policy Block

- SHOULD Error handling implementations SHOULD support both classic and minimal variants to accommodate different performance and bundle size requirements

In scope:
- All public validation API endpoints and exported functions
- Error message structures returned to external API consumers
- Localization modules for internationalized error messages
- Schema validation and coercion interfaces
- Public type definitions and contracts

Out of scope:
- Internal implementation details not exposed through public APIs
- Private utility functions and helpers
- Development and testing infrastructure
- Build and bundling configurations

Exceptions:
- EXC-001: Legacy v3 APIs may use different error structures for backward compatibility
- EXC-002: Minimal/mini variants may omit certain locale support to reduce bundle size

## Rationale

- Pattern detected across 33 files with 90.45% confidence indicates this is an established, intentional architectural decision rather than ad-hoc implementation
- Localization support in multiple languages (ko, pl, kh, mk) demonstrates commitment to international API consumers and user experience
- Separation of concerns between error handling, schemas, and coercion provides clear API boundaries and maintainability
- Multiple version support (v3, v4) and variants (classic, mini) shows evolution of API design while maintaining backward compatibility for external consumers

## Consequences

Positive:
- External API consumers receive consistent, localized error messages improving developer experience and integration success
- Clear separation of error handling, validation, and coercion logic enables independent evolution of each concern
- Structured error contracts facilitate automated error handling and recovery in consumer applications
- Multiple variants (classic/mini) allow consumers to optimize for their specific performance and bundle size requirements

Negative:
- Maintaining multiple locale files increases maintenance burden and requires coordination for new error types
- Supporting multiple API versions and variants increases testing surface area and complexity
- Structured error contracts may be more verbose than simple string messages, potentially impacting payload size
- Backward compatibility requirements may constrain future API improvements and optimizations

## Alternatives

- Use simple string error messages without structured schema or localization (rejected)
  Rejected because: Does not meet internationalization requirements for global API consumers and lacks machine-readable error information for automated handling
  When valid: Only appropriate for internal APIs with English-only audiences
- Implement runtime locale loading with dynamic message resolution (rejected)
  Rejected because: Increases bundle size and runtime overhead; static locale modules provide better tree-shaking and performance
  When valid: Could be reconsidered for server-side only APIs where bundle size is not a constraint
- Use third-party i18n library for error message localization (rejected)
  Rejected because: Adds external dependency and increases bundle size; custom locale modules provide better control and minimal overhead
  When valid: May be appropriate if extensive i18n features beyond error messages are required

## Risks

- Locale files may become out of sync with error codes, resulting in missing translations
  Mitigation: Implement automated tests that verify all error codes have translations in all supported locales; use TypeScript types to enforce completeness
  Owner: API Engineering Team
- Breaking changes to error structure could disrupt existing API consumers
  Mitigation: Maintain strict semantic versioning; use API version namespaces (v3, v4); provide migration guides and deprecation notices
  Owner: API Architecture Team
- Performance degradation from complex error handling and localization logic
  Mitigation: Maintain benchmark suite to track performance; provide minimal variants for performance-critical use cases; optimize hot paths
  Owner: Performance Engineering Team

## Implementation Notes

- Organize locale files in a dedicated locales/ directory with ISO language code naming (e.g., ko.ts, pl.ts, kh.ts, mk.ts)
- Define a canonical error message interface/type that all locale modules must implement to ensure consistency
- Use TypeScript's type system to enforce that all error codes are covered in each locale module
- Implement benchmark tests for validation primitives, real-world scenarios, and discriminated unions to track performance impact
- Provide clear documentation on how to add new locales and maintain existing translations
- Consider using code generation or validation tools to ensure locale completeness across all supported languages

## Continuation Context


Verify commands:
- grep -r "export.*locale" packages/zod/src/*/locales/ | wc -l
- find packages/zod/src -name 'errors.ts' -o -name 'error*.ts' | xargs grep -l 'interface.*Error'
- npm run test:benchmarks -- --grep 'primitives|realworld|discriminatedUnion'

Accept when:
- All locale modules export consistent error message structures matching the canonical interface
- Error handling code is separated from validation logic in distinct modules (errors.ts, schemas.ts, coerce.ts)
- Benchmark tests pass with performance metrics within acceptable thresholds
- Public API exports include structured error types and locale modules

## Enforcement

- Verified by: Automated CI pipeline checks for locale completeness using TypeScript type checking
- Verified by: Unit tests verify error message structure consistency across all locales
- Verified by: Integration tests validate public API error contracts
- Verified by: Benchmark suite runs in CI to detect performance regressions
- Violation handling: CI build fails if locale modules are incomplete or inconsistent
- Violation handling: Pull requests adding new error codes must include translations for all supported locales
- Violation handling: Breaking changes to error structure require major version bump and API review
- Violation handling: Performance regressions beyond threshold trigger automatic review and investigation
- Exception process: Request exception through API Architecture Team review process
- Exception process: Document rationale and impact assessment in ADR or RFC
- Exception process: Obtain approval from at least two senior engineers
- Exception process: Update public documentation to reflect exception and limitations