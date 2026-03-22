# SECURITY PROFILE MATRIX

## Purpose
This matrix helps estimate an app's security level pragmatically before a security implementation or review.

## Procedure
Assess the app along these axes:

### 1. Data Criticality
- low: hardly any sensitive data, no personal data, or only low-critical content
- medium: normal customer, contact, operational, or business data
- high: especially sensitive personal data, financial data, HR data, health data, contract data, credentials

### 2. Exposure
- low: local or internal only, strongly restricted access
- medium: login-protected web app or API
- high: publicly reachable internet app, open integrations, webhooks, mobile clients, many external entry points

### 3. Permission Complexity
- low: no login or only very simple role logic
- medium: users, admins, simple teams, or normal CRUD permissions
- high: multi-tenant, support roles, service accounts, delegation, approvals, tenant and object boundaries

### 4. Side Effects and Abuse Potential
- low: read-only system with no critical actions
- medium: normal write operations, uploads, email, PDFs, exports
- high: invoices, payments, automations, bulk changes, integrations, agents, tools with write access

### 5. Damage in Case of Incident
- low: limited operational damage
- medium: real business interruption, data loss, or reputational damage
- high: major legal, financial, or operational impact

## Classification

### S1
If almost everything is low and no clearly high-risk factor is present.

### S2
As soon as several axes are medium or one single axis becomes clearly production-relevant.
This is the typical default for most real business apps.

### S3
As soon as at least one axis is highly critical and the app is also production-facing, internet-exposed, role-complex, or integration-heavy.
Multi-tenant products with sensitive data or agentic systems with tool access usually belong here as well.

## Decision Rules
- When in doubt, prefer S2 over S1.
- Do not use S3 inflationarily, but take it seriously.
- A low risk class does not justify sloppy implementation.
- A high risk class justifies additional complexity only where it reduces real risk.

## Minimum Measures Per Level

### S1
- safe inputs and outputs
- no obvious injection or XSS flaws
- up-to-date dependencies
- no secrets in code or frontend
- clean error handling
- secure configuration

### S2
- everything from S1
- clean authentication and server-side authorization
- rate limits where sensible
- review upload, export, and integration paths
- test tenant and role logic where present
- dependency and supply-chain hygiene
- make important actions traceable

### S3
- everything from S1 and S2
- formalized threat-model review
- stricter role and tenant separation
- explicitly test abuse scenarios
- stronger secret and session hardening
- better audit logs and alerting
- security gates before release

## Required Question Before Additional Hardening
Does this measure materially reduce a realistic risk for this app?
If not, do not add it blindly.
