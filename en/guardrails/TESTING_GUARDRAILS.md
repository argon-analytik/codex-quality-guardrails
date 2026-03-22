# TESTING GUARDRAILS

## Purpose
This project should not only look good, feel secure, or be structured cleanly, but also work correctly under real conditions.
Testing exists to verify critical behavior, catch regressions early, and release changes with traceable confidence.

The goal is not to produce as many tests as possible.
The goal is to verify the right things in a risk-based way and reliably protect critical logic, state transitions, permissions, error paths, and integrations.

## Core Principles
- verification before gut feeling
- critical paths before test volume
- behavior before implementation
- risk before dogma
- reproducibility before informal clicking
- regression protection before one-off validation
- clear test boundaries before messy overlap
- pragmatism before test bureaucracy

## Core Rule
Not every change needs the same test depth.
The test scope must match criticality, complexity, change risk, and potential impact.

More coverage is needed for:
- auth, session, and permission logic
- multi-tenant separation
- invoices, payments, PDF generation, exports
- imports, data migrations, and data conversion
- background jobs, queues, schedulers, webhooks
- third-party integrations
- state machines and workflow transitions
- critical forms with validation
- destructive actions
- security-relevant changes
- complex refactoring

Less coverage is acceptable for:
- purely visual detail fixes with no behavior change
- small text or copy adjustments
- local helper functions with no operational relevance
- prototypes with no production ambition

## What Should Be Verified
Review in particular:
- expected behavior for valid input
- error behavior for invalid input
- edge cases and boundary values
- state transitions
- permission boundaries
- empty states and null cases
- integration failures
- retry, timeout, and idempotency behavior
- import/export consistency
- persistence and data integrity
- regression risks after refactoring
- multi-user or multi-tenant isolation
- behavior under partial failures
- manual user flows with high criticality

## What Should Be Avoided
- no test volume as an end in itself
- no fragile tests that only verify wired internal details
- no snapshot floods with little real value
- no end-to-end tests for every tiny thing
- no unit tests for trivial boilerplate
- no silent gaps in critical business logic
- no purely manual approval for risky changes when automation would be possible
- no fake confidence from shallow happy-path checks

## Test Types and Usage
Use the right level depending on risk and structure.

### Unit Tests
For pure logic, calculations, parsers, mappers, validation, state transitions, helper functions, and deterministic rules.
Unit tests should be fast, clear, and focused.

### Integration Tests
For the interaction of multiple layers or components, for example:
- route + validation + business logic + data access
- service + third-party integration
- form + API + persistence
- job + queue + state change

### End-to-End Tests
For a few critical user flows with high value or high risk.
For example:
- login
- permission-relevant actions
- creating and exporting an invoice
- multi-step wizards
- critical admin actions
- checkout or approval flows

### Manual Verification
Useful for:
- visual changes
- accessibility review
- browser-specific behavior
- PDF or print rendering
- integrations that are hard to automate
- post-deploy checks

Manual checks do not replace automatable protection for critical logic.

## Focus on Behavior
Tests should protect behavior, not guess at internal implementation.
Prefer:
- input -> expected output
- action -> expected state
- error case -> expected handling
- role X may, role Y may not
- event -> expected consequence
- persistence -> expected data shape

Avoid tests that break for no good reason during harmless refactors.

## Critical Review Areas
Pay special attention to:
- authorization and ownership
- multi-tenant leaks
- state changes and immutability
- calculations and rounding logic
- date, time, and timezone logic
- retry and deduplication logic
- imports with broken data
- exports, PDFs, emails, webhooks
- error paths and fallbacks
- race conditions and double execution
- idempotency for repeated requests or jobs
- filtering, search, pagination, and sorting in complex data views

## Test Data and Isolation
Test data should be controlled, traceable, and as stable as possible.
Avoid:
- hidden dependencies on production-like systems
- volatile external state without a stub or mock
- hard-to-reproduce randomness
- shared, uncleared test state

## Refactoring and Tests
Larger refactors without verification are incomplete.
When structure changes, actively review:
- which existing logic is exposed to regression
- which tests need to be adjusted
- which new tests are required
- whether previously untestable logic was made testable

## Release-Relevant Verification
Before risky releases or production changes, targeted smoke checks should exist.
These should cover at least critical core paths, permissions, jobs, integrations, and the main visible functionality.

## Quality of AI-Generated Tests
AI-generated tests are not automatically meaningful.
Review critically:
- whether the test protects the right thing at all
- whether the test would actually fail if the bug existed
- whether the test is too implementation-coupled
- whether edge cases were chosen sensibly
- whether the test merely copies current behavior without validating the domain

## Definition of Done
A testing pass is only good when:
- critical risks were identified explicitly
- suitable test levels were chosen
- relevant error paths and edge cases are covered
- critical changes are more regression-safe than before
- tests protect behavior rather than luck
- manual and automated checks are separated sensibly
- unnecessary test bureaucracy was avoided

## Required Output After Every Testing Pass
At the end, report:
1. which risks or critical flows were reviewed
2. which tests were newly created, adjusted, or deliberately not added
3. which areas were verified automatically vs. manually
4. which gaps or residual risks remain
5. which additional checks would be useful before release

Important:
Do not just produce "more tests."
Understand risk and criticality first, then protect deliberately.
