# DOCUMENTATION GUARDRAILS

## Purpose
This project should not only work, but also be understandable, transferable, maintainable, and operable.
Documentation is not decorative afterthought and not an end in itself. It exists to capture decisions, structure, operations, boundaries, risks, and usage in a way that allows another person to understand the system and continue it safely.

The goal is not to produce as much text as possible.
The goal is to document exactly the information that matters for understanding, operating, changing, debugging, and handing over the system.

## Core Principles
- clarity before the illusion of completeness
- relevance before text volume
- concreteness before marketing language
- structure before a prose landfill
- current documentation before pretty but outdated documentation
- make decisions and boundaries explicit
- write documentation along real usage scenarios
- pragmatism before documentation bureaucracy

## Core Rule
Not everything needs the same amount of documentation.
The scope of documentation should match the risk, complexity, operational relevance, and likelihood of handover.

More documentation is needed for:
- production systems
- multi-user or multi-tenant solutions
- security-relevant functionality
- third-party integrations
- complex deployments
- role and permission systems
- asynchronous processes, jobs, queues, webhooks, automations
- import/export, billing, PDFs, archiving, backups
- anything that becomes expensive when it fails, is misused, or is misunderstood

Less documentation is acceptable for:
- small throwaway prototypes
- local one-off scripts
- isolated helper functions without operational relevance
- purely visual tweaks with no behavior change

## What Should Be Documented
Document in particular:
- purpose and scope of the system or module
- architecture and major building blocks
- responsibilities and boundaries
- data flow and central states
- important assumptions
- configuration and prerequisites
- setup, build, run, deploy
- environment variables and what they mean
- integrations and dependencies
- auth, roles, and security assumptions
- relevant failure cases, limits, and known restrictions
- operational knowledge, runbooks, and recovery
- API behavior, events, jobs, schedulers, webhooks
- data models, state models, or relevant state transitions
- migration or breaking-change notes
- open risks, technical debt, and deliberate trade-offs

## What Should Be Avoided
- no generic AI text deserts with no information value
- no documentation that merely paraphrases the code
- do not explain obvious things at length if they are already clear from the code
- no outdated copy-paste blocks
- no claims such as "simple," "robust," "secure," or "scalable" without concrete qualification
- no marketing language in technical documents
- no fake precision
- no documentation so abstract that it becomes operationally useless

## Target Audiences
Write documentation so it is clear who it is for.
Typical audiences:
- developers
- operators / admins
- your future self
- customers or internal business stakeholders
- integrators
- contributors during onboarding

Do not mix these audiences unnecessarily inside one vague document.
If needed, separate:
- technical reference
- operations documentation
- end-user documentation
- architecture decisions
- handover or setup instructions

## Documentation Types
Use the appropriate form depending on the need.

### README
For entry point, purpose, setup, start instructions, high-level structure, key commands, and links to deeper documentation.

### Architecture Documentation
For system boundaries, major components, data flows, integrations, security assumptions, and central decisions.

### Runbook / Operations Documentation
For deployment, configuration, monitoring, logs, backups, restore, rollback, troubleshooting, known failure modes, and emergency procedures.

### API or Interface Documentation
For endpoints, inputs, outputs, error cases, events, webhooks, auth requirements, idempotency, and side effects.

### ADRs or Decision Notes
For important architecture or technology decisions:
- what was decided
- why
- which alternatives were rejected
- what consequences follow from it

### Change Documentation
For breaking changes, migrations, new configuration, changed security assumptions, or new operational requirements.

## README Rules
A good README should answer at least:
- What is this?
- What is it for?
- In what context is it used?
- How do you start it locally?
- What are the prerequisites?
- Where is the deeper documentation?
- Which limits or quirks matter?

The README is the entry point, not the full encyclopedia.

## Architecture Documentation
Architecture documentation should not consist of empty buzzword fog.
It should make concrete:
- the major building blocks and responsibilities
- the data flow
- central dependencies
- the auth and role model
- synchronous vs. asynchronous parts
- state transitions
- where business logic lives
- which parts are critical
- which boundaries were drawn deliberately

If diagrams help, use them.
But diagrams do not replace precise text.

## Documenting Configuration
Configuration must be documented explicitly and traceably.
Describe:
- which variables or settings exist
- which values are expected
- which defaults apply
- what is optional vs. required
- which values are security-relevant
- what misconfiguration breaks

Do not provide cryptic ENV lists without explanation.

## Documenting Security
Security-relevant aspects should be documented, but without turning documentation into an attack guide.
Document in particular:
- auth and permission model
- trust boundaries
- security-relevant assumptions
- secret handling
- relevant data classification
- rate limits, validation, upload rules, session or token behavior
- backup, restore, and audit behavior
- known residual risks or deliberately unimplemented measures

Do not document:
- actual production secrets
- unnecessarily exploitable internals
- operational details that should only live in a protected context

## Documenting Data Models and States
If data models, state models, or workflow states matter, they must be documented clearly.
Describe:
- relevant fields
- business meaning
- allowed states
- transitions
- invariants
- what is immutable
- what is auditable or versioned
- how error and edge cases are handled

## Documenting Operations and Troubleshooting
Operationally relevant systems need documented answers to:
- How is it started?
- How is it deployed?
- How is it monitored?
- Where are the logs?
- What are the typical failure modes?
- What does a safe rollback look like?
- How do backup and restore work?
- What do you do when an integration fails?
- What do you do when data becomes inconsistent?
- Which checks are required after changes?

## Documentation During Refactoring and Changes
When structure, behavior, interfaces, or operational assumptions change, actively verify whether documentation needs to be updated.
A code change without a documentation check is not a clean finish.

Pay special attention to:
- changed setup steps
- new environment variables
- changed roles or permissions
- new APIs or payloads
- changed data models
- new schedulers, queues, or background jobs
- new risks, limits, or failure modes

## Language and Style
Documentation should be:
- factual
- precise
- concise, but complete enough
- structured
- verifiable
- technically clean

Avoid:
- filler sentences
- repetition
- unclear pronouns
- empty phrases
- claims that cannot be checked

## Quality of AI-Generated Documentation
Any AI-generated documentation must be checked for truth and fit.
Do not invent:
- files
- processes
- deployments
- security mechanisms
- tests
- integrations
- monitoring
- limits
- roadmap commitments

If something is unclear or not implemented, state that clearly.

## Definition of Done
Documentation is only good when:
- it is clear what the system or module is for
- relevant architecture, configuration, and operational logic are understandable
- important decisions and boundaries are explicit
- setup and operations work without guesswork
- changed assumptions and risks were documented
- the text is concrete rather than generic
- the documentation matches the actual implementation
- unnecessary text volume was avoided

## Required Output After Every Documentation Pass
At the end, report:
1. which documents were created or updated
2. which topics were covered
3. which deliberate boundaries, assumptions, or risks were documented
4. what is still intentionally undocumented
5. where the documentation should be maintained going forward

Important:
Do not just add documentation. Also correct, tighten, or remove existing documentation when it is misleading, outdated, or redundant.
