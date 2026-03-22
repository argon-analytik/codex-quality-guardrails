# ACCESSIBILITY GUARDRAILS

## Purpose
This product should not only look visually polished, but also remain robust and understandable for real people to use.
Accessibility ensures that interfaces stay meaningfully usable with a keyboard, screen reader, zoom, reduced motor control, limited vision, or altered presentation.

The goal is not to tick off formal compliance.
The goal is to systematically improve real usability, clarity, and technical accessibility.

## Core Principles
- usability before visual tricks
- semantics before div soup
- keyboard before mouse assumptions
- clarity before purely visual encoding
- robust interaction before decorative animation
- correct states before visual illusion
- real readability before aesthetic harshness
- pragmatism before ARIA theater

## Core Rule
Accessibility is not only relevant for large public projects.
Even internal or smaller apps benefit greatly from correct keyboard support, clear error messages, sensible focus management, and readable structure.

More care is required for:
- customer-facing or public interfaces
- form-heavy UIs
- data-rich dashboards and tables
- complex dialogs, drawers, menus, and multi-step flows
- admin or operations interfaces with high information density
- apps with frequent keyboard usage
- projects with regulatory or contractual sensitivity

## What Should Be Reviewed and Improved
Pay particular attention to:
- keyboard navigation
- visible focus states
- semantic structure
- form labels and error messages
- contrast and readability
- control sizes and hit targets
- sensible interaction and focus order
- dialog and menu behavior
- screen-reader-relevant states
- zoom and responsive behavior
- meaning that is not conveyed by color alone
- status messages for asynchronous actions

## What Should Be Avoided
- no mouse-only interaction
- no invisible or barely visible focus states
- no ARIA attributes used as alibis without correct semantics
- no interaction that is only understandable through color or position
- no error messages without context or association
- no modal dialogs without focus management
- no tiny hit targets
- no excessive motion without respecting reduced-motion preferences

## Structure and Semantics
Prefer real semantic elements where they fit:
- `button` instead of a clickable `div`
- `label` instead of a bare placeholder
- heading structure instead of purely visual titles without hierarchy
- lists, tables, and landmarks where they are actually appropriate

Semantics are part of usability, not just HTML aesthetics.

## Keyboard and Focus
All essential interactions must be reachable and meaningfully usable by keyboard.
Pay attention to:
- logical focus order
- visible focus
- no focus traps
- correct focus return after dialogs or menus
- Enter, Escape, and Tab behavior for common controls
- no hidden but focusable elements
- no important actions that are only visible or reachable on hover

## Forms and Error States
Forms must be understandable and resilient to errors.
Pay attention to:
- clear labels
- supporting help text where needed
- understandable error copy
- errors placed directly at the relevant field or area
- sensible loading, success, and failure states
- required fields not marked by color alone
- no placeholders used as the only label replacement

## Contrast, Readability, and Scaling
The UI must remain readable under real conditions.
Check:
- sufficient contrast
- typography that is large enough and calm enough
- scaling under browser zoom
- no clipped text or controls when zoomed
- usable layouts at enlarged display sizes
- no click targets that are too small

## Dynamic UI and Status Communication
In asynchronous or dynamic UIs, it must stay clear what is happening.
Pay attention to:
- understandable loading states
- success and error status messages
- sensible live regions where needed
- no silent changes without feedback
- accessible dialogs, menus, tabs, accordions, and drawers

## Tables, Filters, and Data-Rich UIs
For complex data views, review:
- sensible table structure
- readable columns and headers
- focus and keyboard behavior
- accessible filtering and sorting
- understandable empty states
- no color-only encoding for critical differences

## Motion and Preferences
Animation must not make the product harder to use.
Keep in mind:
- respect reduced motion where appropriate
- do not convey important information only through animation
- avoid excessive motion that hurts orientation or readability

## Quality of AI-Generated Accessibility
AI tends to "simulate" accessibility superficially.
Review critically:
- whether the semantics are actually correct
- whether ARIA is both correct and necessary
- whether focus management really works
- whether error messages are understandable and well associated
- whether accessible interaction was actually tested or verified

## Definition of Done
An accessibility pass is only good when:
- core interactions are usable by keyboard
- focus is visible and meaningfully managed
- semantics and structure are understandable
- forms are clearer and more resilient to user error
- contrast and readability are usable
- dynamic states are communicated understandably
- barriers were reduced without making the UI unnecessarily complicated

## Required Output After Every Accessibility Pass
At the end, report:
1. which accessibility problems were reviewed
2. what was improved directly
3. which areas should still be verified manually
4. which barriers or residual risks remain
5. which accessibility topics were deliberately postponed

Important:
Accessibility is not purely visual fine-tuning.
It is part of quality, robustness, and real usability.
