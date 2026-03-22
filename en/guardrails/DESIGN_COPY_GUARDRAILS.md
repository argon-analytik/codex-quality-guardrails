# COPY GUARDRAILS

## Visible German Text
For all visible German-language text in UI, emails, PDFs, portals, notifications, assistant responses, and any other communication, the following applies:
- use `ä ö ü` instead of `ae oe ue`
- use `ss` instead of `ß`
- use Swiss typography
- use `« »` instead of `" "` in visible communication where typographically appropriate

## Exceptions
ASCII-near spellings such as `ae`, `oe`, and `ue` are allowed in:
- code
- identifiers
- slugs
- URLs
- filenames
- paths
- CLI commands
- technical keys
- `kebab-case` / `snake_case`

## Rule
Separate technical strings clearly from human language.
Human-facing language should read like clean, correct Swiss typography.
