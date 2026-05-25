# Adopt Zod Schema Validation for Runtime Type Safety: Performance Critical Validation

Status: proposed
Date: 2024-01-09
Deciders: Detection Pipeline (automated)

## Activation

This ADR is ACTIVE for all TypeScript/JavaScript codebases handling external data inputs, API boundaries, configuration parsing, and user-submitted content.

## Context

- TypeScript provides compile-time type safety but offers no runtime validation, creating a security gap at system boundaries where external data enters the application
- The codebase shows extensive adoption of Zod validation library across 69 files with 92.99% confidence, indicating a mature pattern for runtime type checking and input validation
- Test files demonstrate comprehensive validation scenarios including async refinements, error handling, codec transformations, and locale-specific validation rules
- Benchmark files indicate performance considerations are actively monitored for validation operations across different data types (datetime, string, union, object)
- The pattern spans multiple Zod versions (v3, v4 classic, v4 mini) suggesting long-term commitment and evolution of the validation strategy

## Problem Statement

Without runtime validation, TypeScript applications are vulnerable to type confusion attacks, injection vulnerabilities, and data corruption when processing external inputs. Static type checking cannot protect against malicious or malformed data at runtime, creating a critical security gap at API boundaries, configuration parsing, and user input handling points.

## Decision

1. SHOULD: Performance-critical validation paths SHOULD be benchmarked to ensure validation overhead remains acceptable

## Policy Block

- SHOULD Performance-critical validation paths SHOULD be benchmarked to ensure validation overhead remains acceptable

In scope:
- All HTTP API endpoints receiving external requests
- WebSocket message handlers processing client data
- Configuration file parsers (JSON, YAML, environment variables)
- Database query results from untrusted sources
- Third-party API response processing
- User-uploaded file content parsing
- GraphQL resolvers handling input arguments

Out of scope:
- Internal function calls between trusted modules within the same service
- Type-safe database ORM operations with compile-time schema validation
- Static configuration constants defined at build time
- Unit test mock data with known valid structure

Exceptions:
- EXC-001: Performance profiling demonstrates validation overhead exceeds 10% of request processing time for high-throughput endpoints
- EXC-002: Legacy endpoints scheduled for deprecation within 90 days

## Rationale

- Pattern detected across 69 files with 92.99% confidence indicates this is an established, proven practice within the codebase
- Zod provides TypeScript-first schema validation with excellent type inference, reducing duplication between runtime checks and compile-time types
- Comprehensive test coverage (async refinements, error handling, locales, codecs) demonstrates mature validation practices and edge case handling
- Active benchmarking of validation performance shows awareness of runtime costs and commitment to maintaining acceptable overhead

## Consequences

Positive:
- Eliminates entire classes of injection vulnerabilities (SQL injection, XSS, command injection) by validating and sanitizing inputs at boundaries
- Provides clear, structured error messages for invalid inputs, improving API usability and debugging
- Type inference from Zod schemas ensures runtime validation stays synchronized with TypeScript types, reducing maintenance burden
- Centralized validation logic in schemas makes security audits more tractable and reduces scattered validation code

Negative:
- Adds runtime performance overhead for validation operations, particularly for large payloads or complex nested schemas
- Increases bundle size by including Zod library and schema definitions in client-side applications
- Requires developers to learn Zod API and schema composition patterns, adding onboarding complexity
- May create verbose schema definitions for complex data structures, increasing code maintenance surface

## Alternatives

- Use TypeScript type guards and manual validation functions (rejected)
  Rejected because: Manual validation is error-prone, lacks composability, and creates maintenance burden keeping validation logic synchronized with types. No structured error handling.
  When valid: Acceptable for simple internal utilities with minimal validation requirements
- Adopt alternative validation libraries (Yup, Joi, AJV) (rejected)
  Rejected because: Existing codebase has 69 files using Zod with high confidence. Migration would be costly and Zod's TypeScript-first design provides superior type inference.
  When valid: Consider for new greenfield projects if team has strong existing expertise with alternative libraries
- Generate validators from OpenAPI/JSON Schema specifications (deferred)
  Rejected because: Not mutually exclusive with Zod adoption. Could complement Zod for API contract validation.
  When valid: Use in conjunction with Zod for API gateway validation or contract testing scenarios

## Risks

- Performance degradation on high-throughput endpoints due to validation overhead
  Mitigation: Implement performance benchmarks in CI pipeline (as evidenced by benchmark files). Set SLO thresholds and optimize hot paths using Zod's parse vs safeParse strategically.
  Owner: Engineering team with performance monitoring
- Inconsistent validation coverage leaving security gaps at some boundaries
  Mitigation: Implement static analysis to detect unvalidated external inputs. Add linting rules requiring Zod validation at API route handlers. Conduct security-focused code reviews.
  Owner: Security team and engineering leads
- Schema drift where validation schemas become out of sync with actual data requirements
  Mitigation: Co-locate schemas with API definitions. Use integration tests validating real-world data samples. Implement schema versioning for API evolution.
  Owner: API platform team

## Implementation Notes

- Start by identifying all external data entry points (API routes, config parsers, message handlers) and prioritize based on security risk
- Create reusable schema primitives for common patterns (email validation, UUID formats, date ranges) to ensure consistency
- Use Zod's .safeParse() method at boundaries to handle errors gracefully, reserving .parse() for internal validated data
- Leverage Zod's .transform() and .refine() methods to encode business logic validation rules directly in schemas rather than scattering validation across application code
- Monitor validation performance using the benchmark patterns found in packages/bench/* and optimize schemas showing performance issues

## Continuation Context


Verify commands:
- grep -r "z\.object\|z\.string\|z\.number" --include="*.ts" --include="*.tsx" | wc -l
- grep -r "safeParse\|parse" --include="*.ts" --include="*.tsx" packages/ | grep -v test | wc -l
- npm test -- --testPathPattern=".*\.test\.ts$" --testNamePattern="validation|schema|zod"

Accept when:
- All API endpoint handlers include Zod schema validation before processing request bodies
- Validation test coverage exceeds 80% for all schema definitions with edge cases tested
- Performance benchmarks show validation overhead under 5ms for typical request payloads
- Security scan confirms no unvalidated external inputs at system boundaries

## Enforcement

- Verified by: Automated static analysis scanning for unvalidated external inputs at API boundaries
- Verified by: Code review checklist requiring Zod validation for all new endpoints
- Verified by: CI pipeline integration tests validating schema coverage
- Verified by: Security audit reviews of validation patterns quarterly
- Violation handling: CI pipeline fails if new API endpoints lack corresponding Zod schema validation
- Violation handling: Security team notified of violations detected in production code
- Violation handling: Pull requests blocked until validation coverage meets requirements
- Violation handling: Post-incident reviews for security issues trace back to validation gaps
- Exception process: Submit exception request to security team with justification and alternative controls
- Exception process: Document performance profiling data if requesting performance-based exception
- Exception process: Obtain written approval from engineering manager and security lead
- Exception process: Add exception documentation to ADR exceptions registry with expiration date
- Exception process: Schedule quarterly review of all active exceptions