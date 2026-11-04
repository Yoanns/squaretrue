# TypeScript / React pack

**Applies to:** web front ends written in TypeScript with React.

*Example pack: an illustration, not supported ecosystem coverage.*

## Detect

- `package.json` lists `react` as a dependency.
- `tsconfig.json` is present, or `typescript` is a dependency.
- `*.tsx` source files.

## Core obligations

### Manage resources safely

- Every effect that subscribes, sets a timer, or starts a request returns a cleanup function.
- Cancel in-flight requests on unmount or input change (`AbortController`) so stale responses do not overwrite newer state.

### Preserve concurrency safety

- Treat state as immutable; derive values during render instead of syncing them through effects.
- Use functional updates (`setX(prev => ...)`) when the next state depends on the previous one.
- Guard against out-of-order async results (abort, or compare a request id).

### Access data safely

- Validate data from the network at the boundary, with the project's existing validator if there is one; a TypeScript type is not a runtime check.
- Never render untrusted HTML; avoid `dangerouslySetInnerHTML` unless it is sanitized with the project's sanitizer.
- Authorization is enforced by the server; hiding a button is not access control.

### Verify changes

- Use the package manager whose lockfile is committed (`package-lock.json`, `pnpm-lock.yaml`, `yarn.lock`, `bun.lockb`) and the scripts in `package.json` (`build`, `test`, `lint`, `typecheck`).
- Run the type check as well as the tests; many bundlers skip type errors.
- In component tests, query by role and accessible name (Testing Library) rather than by class or test id where possible.

### Maintain UI consistency

- Reuse the project's design-system components and tokens (CSS variables, theme objects, Tailwind config) instead of literal colors and spacing.
- Use semantic elements (`button`, `a`, `label`, `form`), associate every input with a label, and return focus correctly when dialogs close.

## Pitfalls

- **Stale closures:** effect and callback dependency arrays must list what they read; follow the lint rule instead of silencing it.
- **StrictMode double effects in development:** a bug that only appears there usually means a missing cleanup.
- **Index as `key`** in lists that reorder or filter: state gets attached to the wrong row; use a stable id.
- **`any` and non-null `!`:** they turn off the checks you rely on; narrow the type instead.
- **Dates and time zones:** `new Date('2026-11-04')` is UTC midnight and can show the previous day locally; use the project's date library or explicit formatting.
