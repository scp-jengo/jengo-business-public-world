# Contributing

This repo accepts contributions of generic world patterns — templates, schemas, and structural patterns that any Jengo instance could use. It does not accept org-specific data.

## What belongs here

- Improved or additional YAML templates for registering world entities
- JSON Schema improvements or additions
- New patterns for world model maintenance
- Documentation improvements

## What does not belong here

- Any actual project, service, or person data
- Anything specific to a particular organization or deployment
- Credentials, tokens, environment URLs, or secrets of any kind
- Entries that only make sense for one specific team

If you find yourself writing something that contains real names, real URLs, or real configuration values, it belongs in a private world repo, not here.

## How to contribute

1. Fork the repo
2. Create a branch: `git checkout -b pattern/better-service-map` or `template/tool-template`
3. Make your changes
4. Ensure any new schema is valid JSON Schema draft-07
5. Ensure any new template is generic enough to apply to any project or service
6. Open a pull request with a clear description of what the pattern or template covers and why it is useful

## Template standards

Templates should:
- Use YAML with clear field names and inline comments explaining each field
- Cover the common case without being exhaustive
- Mark optional fields clearly
- Be immediately usable after forking — no placeholders that require guessing

## Schema standards

Schemas should:
- Target JSON Schema draft-07 (`$schema: http://json-schema.org/draft-07/schema#`)
- Define `required` fields explicitly
- Use `enum` for fields with a fixed set of valid values
- Include a `description` on every field

## Pattern standards

Patterns should:
- State the problem they solve in the first paragraph
- Be concrete enough to act on
- Connect to the agent use case — why does an AI agent need this?
- Stay under 400 words unless the complexity genuinely warrants more

## Review

Pull requests are reviewed for:
- Generic applicability (works for any Jengo instance, not just one)
- Template quality (clear, immediately usable)
- Schema validity
- No accidental inclusion of real data
