# REFACTORING GUARDRAILS

## Purpose
This project should remain technically clear, maintainable, robust, and understandable.
Refactoring is not a cosmetic activity. It exists to reduce complexity, lower risk, improve reuse, and make changes safer.

The goal is not to rewrite code for no reason.
The goal is to improve structure, responsibilities, naming, data flow, ownership, and failure modes so that the system becomes easier to understand, test, extend, and operate.

## Core Principles
- simplicity before cleverness
- readability before brevity
- clear responsibilities before implicit mush
- explicit data flows before hidden side effects
- small, well-named building blocks before large multipurpose blocks
- shared primitives before copy-paste
- stable interfaces before chaotic pass-through logic
- pragmatism before dogma

## What Refactoring Should Achieve
Refactoring should in particular:
- reduce unnecessary complexity
- separate responsibilities cleanly
- consolidate repeated code
- make implicit logic explicit
- handle risky edge cases more cleanly
- sharpen naming
- make modules, files, and components more intentional
- improve testability
- pay down technical debt deliberately
- make future changes cheaper and safer

## What Should Be Avoided
- no broad rewrites without clear benefit
- no abstract architecture games without concrete need
- no extra layers just to look "clean"
- no new complexity in the name of reusability
- no premature abstraction
- no refactors that change behavior unintentionally
- no silent API breaks without explicit adjustment
- no new patterns just because they are fashionable

## Typical Problems That Should Be Found and Fixed
Review specifically for:
- oversized files or functions
- unclear or mixed responsibilities
- duplicated or nearly duplicated logic
- copy-paste with slight variation
- cryptic or misleading names
- logic chains with too many nested conditions
- implicit state
- too many boolean flags acting as a hidden state machine
- unclear side effects
- overly broad components or services
- UI components with too much business logic
- backend routes with validation, business logic, and persistence in one block
- missing boundaries between domain, transport, presentation, and storage
- tight coupling
- unnecessary global dependencies
- magic strings, numbers, and one-off constants
- hard-to-test functions
- unclear error handling
- dead paths, legacy leftovers, and unused helpers
- data models that do not match the actual domain

## Structure and Modularity
Structure code around real responsibilities, not around accident or growth history.
A file, component, or class should have one clearly recognizable main job.
If a module orchestrates, validates, transforms, renders, and persists at the same time, the structure is probably wrong.

Prefer:
- small, focused modules
- clear boundaries between layers
- consistent folder and file structures
- stable public interfaces
- internal helpers only where they semantically belong

## Naming
Naming is part of architecture.
Names must make intent, role, and level clear.
Avoid:
- generic names such as `data`, `util`, `helper`, `manager`, `thing`, `handleStuff`
- names that describe implementation rather than meaning
- abbreviations that only make sense locally

Prefer names that:
- are precise in the domain
- draw responsibility clearly
- make inputs and outputs understandable
- make side effects visible where they exist

## Functions and Methods
Functions should be clear, readable, and focused.
If a function mixes several mental levels, it is too broad.
If a function cannot be named meaningfully, it is usually too diffuse.

Pay attention to:
- manageable length
- clear inputs and outputs
- as few hidden side effects as possible
- early validation
- understandable error paths
- reduced nested logic
- extraction of real subtasks, not artificial mini-functions

## Components and Frontend Structure
On the frontend, presentation, state, data loading, and side effects should not be mixed unnecessarily.
UI components should primarily remain UI.
Complex data logic, mapping, validation, or orchestration belongs in clearly named helper layers, hooks, stores, or services, depending on the architecture.

Pay attention to:
- page components that became too fat
- prop chains without a clear boundary
- scattered state logic
- duplicated mapping or formatting logic
- hard-to-follow `useEffect` chains
- inconsistent form logic
- unclear ownership of data and state

## Backend and Service Structure
Routes, controllers, or handlers should not do everything at once.
Validation, auth, business logic, data access, and external integrations should be separated in a traceable way.

Pay attention to:
- missing input validation
- business logic in controllers
- database logic in the wrong places
- unclear transaction boundaries
- missing error classification
- scattered integration logic
- unclear retry or timeout strategy
- hard-to-follow orchestration

## Data Models and Types
Types, interfaces, DTOs, and models should represent the real system cleanly.
Avoid vague catch-all structures, overly broad types, and shapes that only still exist for historical reasons.

Pay attention to:
- imprecise types
- optional fields without a domain reason
- contradictory data shapes
- mapping chaos between API, domain, and UI
- missing normalization
- magical unions or `any`-like escape hatches

## Error Handling
Error handling is part of architecture.
Errors must neither be swallowed silently nor thrown upward chaotically.
Every important error path should be handled deliberately.

Pay attention to:
- empty catch blocks
- unclear fallbacks
- missing context in logs
- mixed user errors, system errors, and integration errors
- inconsistent error types
- missing return contracts for failure cases

## Configuration and Dependencies
Configuration should be explicit, centralized, and traceable.
Avoid scattered environment access and hard-coded special values.
Also review whether libraries, plugins, or helper building blocks are still worth their complexity.

## Performance and Resources
Refactoring should not just make code "prettier," but also more reasonable.
Check for:
- unnecessary re-renders
- unnecessary data loading
- redundant computations
- payloads that are wider than needed
- blocking behavior in the UI
- inefficient loops or N+1-like patterns
- unnecessary serialization or mapping chains

Do not focus on micro-optimization when the actual structure is the main problem.

## Tests and Verification
Important refactors must be verifiable.
If behavior is critical, add or fix tests.
Refactoring without verification is just hope.

Pay attention to:
- fragile tests that verify implementation rather than behavior
- missing tests at critical boundaries
- missing regression coverage for extracted logic
- untestable structures that should first be made testable

## Technical Discipline
Refactoring should address causes, not merely move symptoms around.
Prefer shared solutions in the right place over local workarounds.
If the same problem appears in multiple places, fix the source.

Document important structural decisions briefly and clearly when they are not immediately obvious.

## Definition of Done
A refactoring pass is only done when:
- structure and responsibilities are clearer than before
- complexity was reduced noticeably
- duplicated logic was consolidated
- naming is more precise
- error paths are easier to follow
- central data flows are more understandable
- behavior was preserved or intentionally improved
- critical changes were verified sensibly
- the code is not just different, but actually easier to maintain

## Required Output After Every Refactoring Pass
At the end, report:
1. a short analysis of the main problems
2. what changed structurally
3. which files, modules, or components are affected
4. which duplicates, complexities, or couplings were reduced
5. which risks, open points, or follow-up work remain

Important:
Do not restructure blindly.
Intervene only where the benefit is clear.
Understand first, then cut.
