# Domain references

Load only the sections the change touches. These are prompts, not a universal checklist; project rules take precedence.

## Frontend / UI

Concerns: semantic controls, responsive layout, keyboard operation, focus, and loading, empty, error, success, and restricted states.

Before implementing:
- Read the project's UI conventions (`ui.md` or equivalent).
- Inspect a representative existing screen.
- Identify reusable components and patterns.

While implementing:
- Reuse established components, tokens, and interactions.
- Avoid arbitrary one-off values and interactions.
- Create a shared pattern only when there is a justified need.
- Never silently redesign navigation, branding, or established interactions.

Before delivering:
- Check the relevant states and layouts.
- Exercise interaction and keyboard behavior.
- Review terminology against the rest of the app.
- Update `ui.md` if a shared convention changed (as the documentation mode allows).
- Report unverified visual or accessibility behavior honestly. Without the ability to view the UI, say so.

## Backend / API

Concerns: validation at the request boundary, authorization on every entry point (not only in the UI), error responses consistent with existing endpoints and free of internal details, backward compatibility of existing contracts, and parameterized and bounded data access.

## Database

Concerns: constraints that enforce invariants, transactions around multi-step writes, migration impact on existing data (reversibility, locking, backfill), and data integrity. Running migrations against a shared database needs authorization.

## Native / desktop applications

Concerns: resource ownership and cleanup, exception safety, the UI-thread rule and other concurrency constraints, and platform conventions (file locations, DPI, installers, signing).

## Infrastructure

Concerns: configuration, least-privilege permissions, secrets kept out of the repository and logs, and the deployment and recovery implications of each change. Applying changes to shared environments needs authorization.
