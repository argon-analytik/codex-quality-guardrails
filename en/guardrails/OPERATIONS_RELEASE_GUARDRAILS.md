# OPERATIONS / RELEASE GUARDRAILS

## Purpose
This project should not only work locally, but also be deployable, observable, operable, and recoverable in a controlled way.
Operations and release quality ensure that changes do not get pushed blindly into production systems and that outages, misconfigurations, and data problems remain operationally manageable.

The goal is not to build unnecessary enterprise processes.
The goal is to reduce operational risk in proportion to the actual criticality of the system.

## Core Principles
- operational readiness before local convenience
- observability before blind trust
- reproducibility before click-deploys
- safe changes before hectic rollout
- rollback capability before hope
- clear ownership before implicit operational logic
- proportional processes before overengineering
- pragmatic safeguards before release theater

## Core Rule
Not every app needs the same level of operational and release discipline.
The scope must match user count, data criticality, integrations, change frequency, and outage cost.

More operational discipline is needed for:
- production customer-facing or multi-user systems
- third-party integrations
- jobs, queues, webhooks, or automations
- database migrations
- billing, PDFs, exports, archiving
- multi-tenant operation
- sensitive or audit-relevant data
- high release velocity
- low tolerance for failure

Less effort is acceptable for:
- local tools with no external users
- prototypes with no production ambitions
- isolated helper scripts with no operational relevance

## What Should Be Covered
Review in particular:
- build and deploy traceability
- configuration and ENV hygiene
- secret handling
- migrations and their risks
- rollback or recovery options
- logging, monitoring, and health checks
- error detection for jobs, webhooks, and integrations
- backups and restore paths
- post-deploy verification
- release communication and breaking-change notes
- observability of silent partial failures
- safe handling of partial failures

## What Should Be Avoided
- no unnecessary process weight for small solutions
- no manual magic without documentation
- no silent production changes without minimum verification
- no migrations without regard for data integrity
- no releases without observability
- no rollbacks that exist only in theory
- no scattered configuration without a clear source of truth
- no secret leaks in repositories, logs, or example values

## Configuration and Secrets
Configuration must be explicit, traceable, and separable from code.
Document:
- which ENV variables or settings exist
- which are required vs. optional
- which are security-relevant
- which defaults apply
- what misconfiguration breaks

Secrets must not end up in code, frontend bundles, example configs, or logs.

## Build and Deploy
Build and deploy should be reproducible and controlled.
Pay attention to:
- traceable start and build commands
- defined deploy steps
- idempotent or otherwise controlled deploy mechanics
- clean handling of assets, migration steps, and background processes
- clear differences between local, staging, and production

## Migrations and Data Integrity
Changes to data models or persistence are operationally critical.
Check:
- whether migrations are safe and traceable
- whether forward and backward compatibility were considered
- whether rollback is realistic
- whether backfills, reindexing, or data conversion are required
- whether post-migration checks are defined

## Logging, Monitoring, and Health Checks
Relevant systems need sensible observability.
Pay attention to:
- structured logs with enough context
- no sensitive data in logs
- health checks for relevant services
- error detection for silent partial failures
- visibility into job failures, retry loops, queue backlog, or broken integrations
- useful metrics or other observation signals when the risk justifies them

## Backups, Restore, and Recovery
For data-relevant systems it must be clear:
- whether and how backups are made
- which data is critical
- how restore works
- how integrity is verified after restore
- which data or states cannot be replayed cleanly
- which recovery steps are needed after integration or job failures

## Release Discipline
Releases should not only be "deployable," but controllably releasable.
Pay attention to:
- clear release- or merge-relevant checks
- explicit marking of breaking changes
- migration notes
- post-deploy smoke checks
- fallback strategy when problems occur
- staged rollout where risk and context justify it

## Runbooks and Operational Knowledge
Operationally critical systems need documented answers to:
- How is it deployed?
- How is a failure detected?
- How is a job re-triggered?
- How do you react to integration failures?
- How is rollback or restore performed?
- Which checks are required after release?
- Which failure modes are known?

## Quality of AI-Generated Operations Changes
AI must not invent operational mechanisms that do not exist.
Do not claim or document the following unless they are real:
- monitoring
- alerts
- rollbacks
- backups
- migration safety
- blue/green or canary strategies
- retry or recovery logic

If something is missing, it must be named clearly as a gap.

## Definition of Done
An operations/release pass is only good when:
- critical operational risks are visible
- configuration and secrets are handled cleanly
- migrations and data risks are consciously assessed
- relevant observability exists or is clearly named as missing
- post-deploy and recovery checks are clearer than before
- unnecessary process overhead was avoided
- real release risks are either lower or more clearly controlled

## Required Output After Every Operations / Release Pass
At the end, report:
1. which operational or release risks were reviewed
2. what was improved directly
3. which deploy, migration, observability, or recovery topics are affected
4. which risks deliberately remain
5. which checks or runbooks are still missing before a production release

Important:
Do not complicate things by default.
Operational discipline should reduce real risk, not merely look professional.
