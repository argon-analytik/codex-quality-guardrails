<div align="center">

# codex-quality-guardrails

**Pragmatic guardrails and review prompts for building better apps with Codex**

An open collection of guardrails, spawn review prompts, and implementation prompts for design, security, refactoring, documentation, testing, operations/release, and accessibility.

</div>

---

## What This Repository Is About

This repository bundles reusable guardrails for AI-assisted software development with the **Codex Desktop App** and similar coding agents.

The idea is simple:

- **`.md` files** define the durable quality rules for a domain
- **`01_...SPAWN_REVIEW_PROMPT.txt`** starts a pure review pass with subagents
- **`02_...REVIEW_PROMPT.txt`** executes the follow-up pass and incorporates the findings from the spawn review

That creates a clean two-step workflow:

1. **analyze first**
2. **implement deliberately afterwards**

This avoids blind actionism, unnecessary rewrites, and generic AI filler.

---

## Why This Repository Exists

Many AI-generated projects do not fail at the first working version. They fail on quality afterwards.

Typical problems include:

- visually overloaded or inconsistent UIs
- fragile, hard-to-maintain code
- missing or disproportionate security measures
- unclear or outdated documentation
- no real verification of critical logic
- weak operational readiness before production releases
- accessibility that is merely simulated visually instead of actually implemented

This repository is meant to turn that into **a systematic way of working**.

---

## Available Areas

| Area | Purpose | Standard or optional? | Especially useful when |
|---|---|---:|---|
| **Design** | visual calm, consistency, readability, UI/UX polish | Standard | as soon as a UI exists |
| **Copy** | visible language, UI text, typography conventions, locale-specific editorial rules | Standard add-on | together with Design |
| **Refactoring** | structure, naming, maintainability, decoupling | Standard | almost always |
| **Security** | risk-based security review and hardening | Standard | almost always |
| **Documentation** | setup, architecture, operations, handover, assumptions | Standard | almost always |
| **Testing** | verification, regression protection, critical flows | Recommended | for almost any real application logic |
| **Operations / Release** | deploys, migrations, observability, rollback, runbooks | Optional | for production or release-relevant systems |
| **Accessibility** | keyboard use, focus, semantics, readability, genuine accessibility | Optional, but recommended | for public, customer-facing, or form-heavy UIs |

---

## What Should Usually Be Standard

For most serious projects, this core set is sensible:

- `DESIGN_GUARDRAILS.md`
- one locale-specific copy guardrail, for example `DESIGN_COPY_GUARDRAILS_SWITZERLAND.md` or `DESIGN_COPY_GUARDRAILS_GERMANY.md`
- `REFACTORING_GUARDRAILS.md`
- `SECURITY_GUARDRAILS.md`
- `DOCUMENTATION_GUARDRAILS.md`
- `TESTING_GUARDRAILS.md`

These six layers already cover the main quality axes:

- how it feels
- how it is built
- how secure it is
- how well it can be understood and operated
- how well critical behavior is verified

---

## What Is Optional

### Operations / Release

This area is not necessary for every small prototype.

It becomes important as soon as at least one of the following applies:

- production use
- real deployments
- migration risk
- jobs, queues, webhooks, or integrations
- data that becomes expensive or critical when things go wrong
- a need for rollback, health checks, backups, or runbooks

If your project is purely local, small, or disposable, you can often leave this area out.

### Accessibility

Accessibility is **recommended**, but it should be applied consciously.

Why is it optional?

Because accessibility improvements often affect more than colors or labels:

- semantic structure
- focus management
- keyboard navigation
- error messages
- dialog behavior
- form structure
- sometimes even component and layout decisions

That can lead to **real structural design changes**. That is exactly why accessibility is so valuable for public, customer-facing, or form-heavy products, but it should not be treated as a purely cosmetic pass.

Pragmatic rule of thumb:

- **public or customer-facing UIs:** clearly recommended
- **internal tools:** often valuable, but scope it consciously
- **early prototypes:** optional

---

## Workflow Principle

This repository is built around a review-first workflow.

### Phase 1: Spawn Review
Use the matching `01_...SPAWN_REVIEW_PROMPT.txt` first.

Goal:
- have subagents review in parallel
- analyze only
- make no changes
- prioritize findings
- consolidate overlaps

### Phase 2: Implementation Pass
Then use the matching `02_...REVIEW_PROMPT.txt` together with the corresponding `.md` file.

Goal:
- validate spawn findings
- implement confirmed points
- identify additional issues
- clearly state at the end what was confirmed, implemented, rejected, or postponed

---

## Using This with the Codex Desktop App

The repository currently contains German material in `/de` and the English version in `/en`.

Important nuance:

- `/de/guardrails/DESIGN_COPY_GUARDRAILS_SWITZERLAND.md` contains Swiss typographic rules for visible German text, for example guillemets `« »` and `ss` instead of `ß`.
- `/de/guardrails/DESIGN_COPY_GUARDRAILS_GERMANY.md` contains German typographic rules, for example German quotation marks and the use of `ß` according to German orthography.
- Use the copy file that matches your target locale instead of applying one variant blindly.
- If you target Austria or another German-speaking market, adapt the closer German-language variant to that market's rules.
- More generally, every language and country should respect its own typographic conventions.
- The English file `/en/guardrails/DESIGN_COPY_GUARDRAILS.md` is therefore only a base file and should be adapted when your English product follows a specific national or editorial standard.

### 1. Copy the files into your project

Place the guardrails in your repository, for example like this:

```text
/guardrails
  DESIGN_GUARDRAILS.md
  DESIGN_COPY_GUARDRAILS_SWITZERLAND.md
  DESIGN_COPY_GUARDRAILS_GERMANY.md
  REFACTORING_GUARDRAILS.md
  SECURITY_GUARDRAILS.md
  SECURITY_PROFILE_MATRIX.md
  DOCUMENTATION_GUARDRAILS.md
  TESTING_GUARDRAILS.md
  OPERATIONS_RELEASE_GUARDRAILS.md
  ACCESSIBILITY_GUARDRAILS.md

/prompts
  01_DESIGN_SPAWN_REVIEW_PROMPT.txt
  02_DESIGN_REVIEW_PROMPT.txt
  01_REFACTORING_SPAWN_REVIEW_PROMPT.txt
  02_REFACTORING_REVIEW_PROMPT.txt
  01_SECURITY_SPAWN_REVIEW_PROMPT.txt
  02_SECURITY_REVIEW_PROMPT.txt
  01_DOCUMENTATION_SPAWN_REVIEW_PROMPT.txt
  02_DOCUMENTATION_REVIEW_PROMPT.txt
  01_TESTING_SPAWN_REVIEW_PROMPT.txt
  02_TESTING_REVIEW_PROMPT.txt
  01_OPERATIONS_RELEASE_SPAWN_REVIEW_PROMPT.txt
  02_OPERATIONS_RELEASE_REVIEW_PROMPT.txt
  01_ACCESSIBILITY_SPAWN_REVIEW_PROMPT.txt
  02_ACCESSIBILITY_REVIEW_PROMPT.txt
```

Choose or adapt the copy file that matches the language and country you are shipping for.

You can also place the files in the repository root. The important part is that Codex can read them clearly and that the paths stay consistent.

### 2. Choose the relevant area

Do not throw every prompt at every change.

Pick only the areas that are actually relevant.

Examples:

| Change | Sensible areas |
|---|---|
| Reworking a UI | Design, Copy, maybe Accessibility |
| Rebuilding an API | Refactoring, Security, Testing, Documentation |
| Changing auth or roles | Security, Testing, Documentation, maybe Operations |
| Adding a PDF/export flow | Design, Security, Testing, Documentation |
| Production release with migrations | Security, Testing, Operations/Release, Documentation |

### 3. Run `01_...` first

Start with the spawn review.

Typical thinking:
- first the design spawn review
- then the design implementation pass
- only then move to the next area

That is usually better than firing off five implementation prompts in a row immediately.

### 4. Then run `02_...` together with the `.md` guardrails

The `02_...` prompt is meant for actual implementation.

It should:
- take the spawn findings into account
- but **not adopt them blindly**
- validate everything against the current state
- fix additional issues where appropriate
- summarize the final changes cleanly

---

## Recommended Sequences

### For UI-heavy apps

1. Design  
2. Refactoring  
3. Security  
4. Testing  
5. Documentation  
6. Accessibility  
7. Operations / Release

### For backend, API, or integration work

1. Refactoring  
2. Security  
3. Testing  
4. Documentation  
5. Operations / Release  
6. Design only where the UI is affected

### For production releases

1. Security  
2. Testing  
3. Documentation  
4. Operations / Release  
5. Accessibility only if the UI is affected and relevant  
6. Design only if the release includes a visible change

---

## Repository Structure

```text
codex-quality-guardrails/
├─ README.md
├─ de/
│  ├─ guardrails/
│  └─ prompts/
└─ en/
   ├─ README.md
   ├─ guardrails/
   └─ prompts/
```

---

## Design Principles of This Collection

This collection follows a few explicit rules:

### 1. Not everything is always necessary
The guardrails are meant to help you make **targeted** better decisions, not artificially inflate every app.

### 2. Review before implementation
Inspect first, then cut. That applies to design just as much as to security or refactoring.

### 3. Risk before dogma
Not every app needs enterprise-grade security, complete end-to-end coverage, or heavy operational processes.

### 4. No AI wallpaper
Documentation, tests, security hardening, and accessibility should stay concrete, traceable, and actionable.

### 5. Codex needs clear responsibilities
The guardrails define **what** a domain should achieve. The `01_` and `02_` prompts define **how** the corresponding pass should run.

### 6. Copy rules are locale-specific
The copy guardrails are intentionally language- and locale-aware.
In `/de`, there are separate German-language variants for Switzerland and Germany.
If you ship for Austria or another German-speaking locale, adapt the closer variant instead of assuming one file fits all.
The English rules in `/en` are likewise only a base and should be adapted when a product follows a specific national or editorial typographic style.

---

## Who This Is For

This collection is especially useful for:

- solo developers and small teams
- people building productively with Codex or Claude
- apps with growing complexity
- products where "it kind of works" is not enough
- projects that should become cleaner without collapsing into process bureaucracy

---

## What This Collection Is Not

This repository is:

- **not a framework**
- **not a design library**
- **not a security certification**
- **not a replacement for human judgment**
- **not a demand to always run every area at the same time**

It is a set of reusable **working rules and review templates**.

---

## Recommendations for a Public Repository

If you make this repository public, these additions are also useful:

- `LICENSE`
- `CONTRIBUTING.md`
- `CODE_OF_CONDUCT.md` only if you actively expect community contributions
- `examples/` with a few real prompt combinations
- `templates/` for project-specific variants
- `CHANGELOG.md` if the guardrails continue to evolve actively

---

## Recommended Repository Name

**Recommendation:** `codex-quality-guardrails`

Why this name works well:

- broad enough to cover design, security, refactoring, testing, documentation, operations, and accessibility
- immediately understandable
- clearly tied to Codex
- not narrowed to a single area
- readable as a public repository name

Other workable alternatives:

- `codex-review-guardrails`
- `codex-shipping-guardrails`
- `agent-quality-guardrails`

If the focus should explicitly extend beyond Codex, `agent-quality-guardrails` is the more neutral option.

---

## Practical Starting Point

If you do not know where to begin, use this minimal workflow:

1. Design  
2. Refactoring  
3. Security  
4. Testing  
5. Documentation  

Then add, depending on the project:

- Operations / Release for production systems
- Accessibility for public or UI-critical products

---

## License and Usage

You can copy, adapt, and combine these guardrails directly in your own projects.
For a public repository, a simple permissive license is usually the most practical choice.

Typical options:
- MIT
- Apache-2.0

---

## Note

These guardrails are intentionally **pragmatic**.
They are meant to improve real quality, not manufacture artificial complexity.

If you use them, use them as a clean foundation for better judgment, not as dogma.
