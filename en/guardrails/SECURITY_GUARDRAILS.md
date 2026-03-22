# SECURITY GUARDRAILS

## Purpose
These rules are meant to prevent security from being implemented either too weakly or with unnecessary excess.
Not every app needs the same level of hardness. But every app needs a clean, conscious, risk-based security review.

The goal is not maximum complexity.
The goal is a pragmatic, clean security architecture that fits the app.

## Principle
Security is not a generic feature add-on.
Security is a combination of:
- correct threat assessment
- clean architecture
- secure defaults
- robust implementation
- good operational and update processes

Always treat security as risk-based.
Avoid two extremes:
- an implementation that is too weak because classic or modern attack surfaces were overlooked
- unnecessary over-hardening that makes the product, UX, and maintainability worse even though the real risk is low

## Security Procedure Before Every Implementation or Review
Before making changes, determine the app's security profile first:
1. Which data is processed?
2. What realistic harm would result from leakage, manipulation, or abuse?
3. Is the app publicly reachable on the internet or only internal?
4. Are there user accounts, roles, tenants, or admin functions?
5. Are there payments, documents, uploads, PDFs, email, import, export, or integration features?
6. Are there privileged automations, agents, or tools with side effects?
7. What compliance, contractual, or reputational consequences would an incident have?

Only then choose security measures.
Do not add enterprise complexity blindly.
But do not trivialize risk either.

## Security Levels

### Level S1: Low Risk
Examples:
- simple internal tools without sensitive data
- small microsites with no login
- simple dashboards with low criticality

Expectation:
- clean input validation
- secure defaults
- no obvious injection, XSS, CSRF, or auth flaws
- no secrets in code
- up-to-date dependencies
- logging without leaks
- secure configuration

### Level S2: Normal Production Risk
Examples:
- normal web apps with login
- CRUD systems with customer data
- multi-tenant business apps
- portals with uploads, PDFs, email, roles, or APIs

Expectation:
- everything from S1
- clean authentication and authorization
- server-side permission checks
- protection against IDOR/BOLA
- CSRF protection, hardened sessions, rate limits
- safe file handling
- auditability of important actions
- dependency and supply-chain hygiene
- a minimum threat model per feature

### Level S3: High Risk
Examples:
- finance, healthcare, or HR-adjacent systems
- apps with especially sensitive personal data
- admin platforms with high blast radius
- systems with many integrations or broad automation powers
- agentic systems with external tools or write access

Expectation:
- everything from S1 and S2
- formalized threat-model review
- stricter session, secret, and key management
- harder separation of roles, tenants, and trust boundaries
- minimized privileges
- explicit review of abuse cases and misuse scenarios
- hardened infrastructure and deployments
- better audit logs, alerting, and incident readiness
- security gates before release

## Always Review These Points, Regardless of the Level
These items are mandatory even for smaller apps:

### 1. Inputs and Outputs
- do not feed unchecked input into SQL, NoSQL, shell commands, templates, Markdown renderers, PDF renderers, or file paths
- use parameterized queries instead of string concatenation
- validate on the server side, not only in the frontend
- handle output context correctly: HTML, URL, JS, CSS, Markdown, templates, CLI
- keep XSS, injection, path traversal, command injection, and SSRF in mind

### 2. Authentication and Sessions
- no homemade cryptography or session logic
- use established libraries and flows
- choose session and token lifetime deliberately
- set secure cookie flags where cookies are used
- do not trust client-side roles or hidden UI states
- review logout, session invalidation, and password reset carefully

### 3. Authorization
- always check permissions server-side
- never rely on hidden UI alone
- validate object access to foreign records
- explicitly test tenant and role logic
- harden admin functionality separately

### 4. Secrets and Configuration
- no secrets in the repo, frontend bundle, logs, or screenshots
- handle secrets only through secure secret mechanisms or environment management
- separate dev, test, and prod cleanly
- remove debug modes, open admin endpoints, demo credentials, and verbose errors before release

### 5. Dependencies and Supply Chain
- review frameworks, plugins, SDKs, extra modules, and build tools for outdated or vulnerable versions
- remove unnecessary dependencies
- prefer lockfiles and reproducible builds
- check the provenance and trustworthiness of new packages
- do not ignore transitive risks

### 6. Logging and Error Handling
- do not log passwords, tokens, session IDs, API keys, personal content, or internal secrets
- keep user-facing errors reduced, but still useful for internal diagnosis
- do not leak stack traces or internal details to end users

### 7. Transport and Data Storage
- enforce TLS where relevant
- store sensitive data only if it is actually needed
- minimize retention
- also review exports, backups, caches, and temporary files
- assess sensitive data in the browser, local storage, the file system, or mobile caches consciously

## Probe Classic Vulnerabilities Explicitly
Check explicitly for:
- SQL injection
- NoSQL injection
- command injection
- XSS
- CSRF
- SSRF
- path traversal
- insecure deserialization
- open redirects
- IDOR / BOLA
- broken access control
- security misconfiguration
- insufficient rate limiting
- file upload abuse
- directory listing or publicly reachable artifacts
- overly broad CORS rules
- missing security headers where relevant
- insecure password reset or invite flows
- session fixation or weak token handling

## Modern and Frequently Overlooked Risks
Also review:
- outdated framework, plugin, or SDK versions
- weak supply-chain hygiene
- dangerous default configurations
- leaks through telemetry, error tracking, analytics, or third-party scripts
- insecure webhooks, callback endpoints, or integrations
- missing tenant isolation
- bypasses via queue workers, cron jobs, background tasks, or internal APIs
- PDF, export, import, or office-document pipelines
- Markdown, rich-text, or template rendering
- signed URLs, presigned uploads, attachment access, and download permissions
- shadow copies of sensitive data in cache, queue, search index, or logs

## File Uploads, Documents, and Generation
As soon as the app supports uploads, PDFs, exports, or document generation, additionally review:
- validate MIME type, file extension, and actual file contents
- enforce file size and limits
- sanitize filenames
- no direct execution or public storage without access control
- clean up temporary files
- no uncontrolled template injection into PDF, HTML, or document generators
- validate download URLs and attachment permissions on the server side

## APIs and Integrations
For APIs, webhooks, and integrations, review:
- authentication and authorization per endpoint
- input validation per endpoint, not just globally
- rate limits, replay protection, or signature checks where relevant
- idempotency for critical write operations
- robust error handling without leaking data
- never trust external responses blindly
- timeouts, retries, and fallbacks designed safely

## Multi-Tenant and Role Models
For multi-tenant apps, this is mandatory:
- validate every query, object access, and export against tenant context
- never accept foreign tenant IDs
- do not model permissions only in the frontend
- distinguish admin, support, service-account, and user roles strictly
- test cross-tenant leaks systematically

## Infrastructure and Operations
Also review the non-visible layers:
- secure default configuration for reverse proxy, app server, database, and storage
- no unnecessarily open ports, buckets, queues, or admin panels
- keep deployments reproducible
- allow secret rotation at least for critical systems
- treat backups as encrypted and access-protected
- provide monitoring and alerting for security-relevant incidents

## Agentic, AI, or Tool-Assisted Systems
If the app uses agents, tools, LLMs, or automated actions, additionally review:
- strict separation between reading, deciding, and acting
- give tools only the minimum required permissions
- no implicit tool calls without a clear policy
- consider prompt injection, context manipulation, and tool abuse
- never treat external content as trustworthy by default
- explicitly protect and log actions with side effects
- never pass secrets into prompts, context, or model outputs unfiltered
- respect different trust levels for user input, retrieved content, system instructions, and tool output

## Pragmatism Rule
Not every app needs MFA, hardware keys, exhaustive audit trails, or complicated approval workflows.
But every production app needs a clean minimum review.

Therefore:
- baseline protection always
- additional hardening based on the risk profile
- raise complexity only where the harm, exposure, or abuse potential justifies it

## Release Gate Before Production
Before release, verify at least:
1. the security level was determined and justified
2. the key trust boundaries are documented
3. classic vulnerabilities were checked
4. authorization and tenant boundaries were tested
5. secrets, logs, and error output were reviewed
6. dependencies and outdated components were reviewed
7. upload, export, PDF, email, and integration paths were reviewed, if present
8. residual security issues were documented

## Required Output After Every Security Review
At the end, report:
1. the app's security level and a short justification
2. the key risks by likelihood and impact
3. concrete findings
4. what was fixed directly
5. what is consciously accepted and why
6. which points must still remain open or be tested before release

## Important
Do not just tick through checklists.
Understand the security-relevant relationships.
Do not complicate blindly.
But do not downplay risk either.
Work in a risk-based, clean, traceable, and pragmatic way.
