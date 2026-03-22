# DESIGN GUARDRAILS

## Purpose
This product should feel visually calm, consistent, readable, and intentionally structured.
UI work is not decoration. It is information architecture, hierarchy, spacing, typography, interaction clarity, and visual consistency.

The goal is not a redesign for its own sake.
The goal is to deliberately polish, simplify, align, and normalize the existing product so it feels intentional and production-ready.

## Core Principles
- clarity before density
- consistency before variety
- simplification before additional UI
- shared components and design tokens before one-off solutions
- clear hierarchy before oversized type
- calm spacing before cramped layouts
- obvious interaction before explanatory clutter

## What Should Be Reviewed and Improved
Review all relevant views, dialogs, sidebars, split panes, detail views, forms, tables, cards, portals, and states in the browser.

Find and fix, in particular:
- overloaded forms
- inconsistent spacing
- poorly aligned elements
- overlapping UI
- typographically unbalanced copy
- text that is too large, too small, or poorly proportioned
- inconsistent padding, radius, shadow, and focus styles
- broken selected, outline, or border rendering
- containers or inner boxes that touch other elements instead of breathing
- poor scroll behavior
- split-pane layouts where areas do not scroll independently
- component mismatch
- font mismatch
- visual noise from too many borders, boxes, and nested containers
- unnecessary text labels on obvious actions
- poor use of horizontal space
- weak responsive behavior

## Layout and Spacing
Normalize the layout with a coherent spacing system.
Use consistent gaps, padding, margins, and vertical rhythm.
Avoid cramped controls, but also avoid pointless empty space.
Cards, panels, and groups must have clean internal padding and clear separation from neighboring elements.
Decorative inner borders or rounded containers must never visually collide with adjacent elements.

## Typography
Define and use a clear type hierarchy across the whole app.
Use a limited, consistent scale for:
- page titles
- section titles
- subtitles
- labels
- body text
- help text
- metadata

Avoid random jumps in size, oversized headings, tiny secondary text, or inconsistent line heights.
Typography should feel calm, readable, and balanced.

Do not mix fonts arbitrarily.
Use the intended font stack consistently across the product.

## Buttons and Actions
Reduce visual noise in action areas.
Where actions are clear from context and space is tight, prefer icon-only buttons with a clean tooltip and `aria-label`.
Do not stack standard actions vertically just because the labels are too wide.
Use compact, consistent action groups with stable size and alignment.

Do not remove text labels if that would make the action unclear.
Use judgment, not dogma.

## Components and States
Unify how components are used.
Do not create multiple almost-identical card, button, input, or badge styles without a real semantic reason.
Normalize hover, focus, active, selected, disabled, loading, empty, and error states.
Selected outlines and focus rings must render cleanly and consistently, without broken corners, uneven thickness, or clipping.

## Forms
Longer forms should be restructured for better scannability.
Group related fields clearly.
Reduce density.
Improve visual hierarchy.
Use progressive disclosure where it helps.
No long compressed walls of controls.

## Scroll and Pane Behavior
Independent scroll areas must work independently where that matches the intended UX.
Avoid scroll traps, coupled scroll bugs, clipped sticky areas, and layouts where one pane blocks another from being usable.

## Visual Character
The UI should feel modern, calm, precise, and functional.
Not flashy.
Not overloaded.
Not playful.
Not visually loud.

## Language and Typography Rules for Visible German Text
For all visible German text:
- use `ä ö ü` instead of `ae oe ue`
- never use `ß`; always use `ss`
- use Swiss typography
- use `« »` in visible communication where typographically appropriate

Exceptions:
- code
- slugs
- identifiers
- URLs
- filenames
- paths
- CLI commands
- technical keys
- `kebab-case` / `snake_case`

## Technical Discipline
Do not hide problems with ad hoc CSS if the real cause sits in a shared component, token, or layout rule.
Prefer clean fixes at the source.
Where it makes sense, consolidate repeated one-off solutions into shared primitives, tokens, or shared components.

Do not introduce a new design language unless that was explicitly requested.
Work within the existing product language and improve it.

## Accessibility and Robustness
Preserve readable contrast, sensible hit targets, keyboard usability, and visible focus states.
Visual improvements must not damage functionality.

## Definition of Done
A UI/UX polishing pass is only done when:
- no obvious overlaps remain
- spacing and typography feel coherent across screens
- components look related rather than improvised
- selected and focus states render cleanly
- forms are more readable and less cramped
- action areas use space efficiently
- scroll behavior works correctly
- visible German text follows the language rules above
- the result feels calmer, cleaner, and more deliberate without losing functionality

## Required Output After Every Polishing Pass
At the end, report:
1. a short audit summary of the main problems
2. what was changed concretely
3. which shared components, tokens, or styles were normalized
4. which residual issues or blockers still remain

Important:
Do not just describe problems. Actually fix them.
