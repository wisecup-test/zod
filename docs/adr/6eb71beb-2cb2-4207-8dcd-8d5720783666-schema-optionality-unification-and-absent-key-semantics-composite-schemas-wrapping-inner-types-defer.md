# Schema Optionality Unification and Absent Key Semantics: Composite Schemas Wrapping Inner Types Defer

Status: proposed
Date: 2026-09-24
Deciders: AI (signal conversion)

## Context

- Inconsistent handling of absent keys versus explicit undefined values introduces discrepancies across object fields, tuple elements, and wrapper schemas such as preprocess, catch, and default.
- Direct missing-key interception previously evaluated outer wrapper schemas before inner schemas could execute fallback or preprocessing logic. A redesign of optionality, catch, and preprocess semantics defers absent-key resolution to inner schemas as codified in wiki/optionality.md.

## Problem Statement

Inconsistent handling between absent keys and explicit undefined inputs in composite schema wrappers causes bypassed fallbacks, unpredictable transforms, and divergent behavior across object properties and tuple elements.

## Decision

1. MUST: Composite schemas wrapping inner types MUST defer absent-key and missing-element resolution down to the inner schemas instead of short-circuiting on undefined or absent input.

## Policy Block

- MUST Composite schemas wrapping inner types MUST defer absent-key and missing-element resolution down to the inner schemas instead of short-circuiting on undefined or absent input.

In scope:
- Core schema definitions under packages/zod/src/v4/core/schemas.ts
- Classic schema definitions under packages/zod/src/v4/classic/schemas.ts
- Composite wrapper schemas including preprocess, catch, tuple, and optionality handling

Out of scope:
- Terminal primitive schemas with no wrapper layers or child schema delegations

Exceptions:
- ex-1: A custom wrapper is explicitly designed to discard absent keys without invoking child schema validation, as documented in an approved RFC.

## Rationale

- Deferring absent-key resolution ensures inner transformations and catch fallbacks are properly executed instead of being bypassed prematurely by wrapper logic.
- Standardizing optionality semantics across object properties and tuple holes eliminates semantic divergences between absent keys and explicit undefined values.
- Centralizing optionality propagation rules according to wiki/optionality.md provides deterministic type inference and runtime validation behavior across composite schemas.

## Consequences

Positive:
- Predictable and uniform handling of absent keys and explicit undefined values across objects and tuples.
- Guaranteed execution of preprocess and fallback handlers in nested schema configurations.
- Clear, documented semantics for composite schema behavior in wiki/optionality.md.

Negative:
- Potential behavioral breakages in schemas that previously relied on outer wrappers short-circuiting absent keys.
- Increased complexity in schema traversal and evaluation pipelines when delegating resolution to inner schemas.

## Alternatives

- Direct missing-key interception where wrapper schemas evaluate before inner schemas can apply catch or preprocessing logic (rejected)
  Rejected because: Causes subtle discrepancies between absent keys and explicit undefined values, prematurely bypassing fallback and transformation handlers defined on inner schemas.
- Strict isolation where absent keys and explicit undefined values are bifurcated into separate schema evaluation paths (rejected)
  Rejected because: Increases schema configuration friction and prevents shared fallback mechanisms like catch and default from resolving omitted fields predictably.

## Risks

- Existing consumers expecting wrapper-level short-circuiting on absent keys may observe altered validation or transform output.
  Mitigation: Validate behavioral parity and migration paths using the comprehensive test suite covering catch, preprocess, tuple, and optionality mechanics.
  Owner: Core Schema Maintainers

## Implementation Notes

- Ensure tuple holes and object properties handle absent elements uniformly.
- Check optin and fallback symbol mechanics when propagating absent keys through schema pipelines.
- Refer to wiki/optionality.md for exact specifications on undefined propagation versus absent key semantics.

## Continuation Context


Verify commands:
- Discover and run the project's test suite for schema validation, catch, preprocess, and tuple optionality.

Accept when:
- Inner schema fallbacks and transforms execute when wrapper schemas receive absent keys or undefined inputs.
- All test cases covering catch, preprocess, partial, tuple, and optional schemas pass without regressions.
- Schema behavior aligns with missing-key resolution specifications in wiki/optionality.md.

## Enforcement

- Verified by: Continuous integration schema test suites covering optionality, catch, partial, tuple, and preprocess execution semantics.
- Verified by: Architectural peer review of wrapper schemas and resolution logic in core and classic schemas.
- Violation handling: Automated CI test failures for wrappers that short-circuit absent keys prior to inner schema delegation.
- Violation handling: Pull request review rejection for implementations deviating from wiki/optionality.md.
- Exception process: Submit a formal RFC detailing why an outer wrapper must short-circuit without inner schema delegation, approved by Core Schema Maintainers.

## References

- file:packages/zod/src/v4/core/schemas.ts
- file:packages/zod/src/v4/classic/schemas.ts
- file:wiki/optionality.md
- file:packages/zod/src/v4/classic/tests/catch.test.ts
- file:packages/zod/src/v4/classic/tests/preprocess.test.ts
- file:packages/zod/src/v4/classic/tests/partial.test.ts
- file:packages/zod/src/v4/classic/tests/tuple.test.ts
- file:packages/zod/src/v4/classic/tests/optional.test.ts
- commit:c2be4f819064eed62c7c350a2d399b5faecd15f8
- commit:1cab69383fcdeae2a366d5e2a2fc4d8fc765d168
- commit:02c2baf7d0d615872fa4528a8020603b71211702
- commit:cede2c63739a5823d6aa5093d291e9a111da943d
- commit:b6066b3e4730fc8b966d13974b4abae8dce25df4
- commit:57d80a82bde8877f3eb79e5dad9786096c37490f
- pr:#5661
- pr:#5900
- pr:#5929
- pr:#5937
- pr:#5939
- pr:#5941