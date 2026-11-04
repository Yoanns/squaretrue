# Documentation procedure

Goal: an unfamiliar developer, or the original one returning years later, can understand, run, inspect, and safely change the system without old conversations.

## 1. Apply the mode

| Mode | Writes |
|---|---|
| `report-only` | No documentation files. Notes, decisions, and gaps go in the delivery report. No claim of durable documentation. |
| `existing-only` | Only into documentation files that already exist. Create none. Disclose missing coverage in the delivery report. |
| `full` | Maintains the structure below, creating a file only when it has real content. The only mode that aims to pass the five-year return test. |

Whatever the mode does not allow you to write goes in the delivery report.

## 2. Structure (`full`)

```text
README.md
docs/
  architecture.md
  development.md
  ui.md
  decisions.md
  features/
    <meaningful-feature>.md
```

Reuse an existing structure where it fits. Small projects may combine sections; large ones may split them. Never create an empty file.

| Document | Holds |
|---|---|
| `README.md` | Purpose, status, capabilities, quick start, navigation to the other docs |
| `architecture.md` | Components, responsibilities, dependencies, data flows, trust boundaries |
| `development.md` | Prerequisites, setup, configuration, initialization, build/test/run |
| `ui.md` | The UI contract (section 6) |
| `decisions.md` | Significant decisions (section 4) |
| `features/` | Feature behavior, business rules, implementation map, verification references |

Each decision lives only in `decisions.md`, and each shortcut only in its code comment. Other documents link to them instead of restating them, except to state a shortcut's system-level consequence.

## 3. Update what changed

1. Explain the implemented behavior.
2. Update affected setup, architecture, UI, and operational guidance.
3. Record significant decisions (section 4) and shortcut consequences (section 5).
4. Check documented commands, paths, and links where practical; disclose untested setup steps and examples.
5. Remove or correct descriptions the change made obsolete.

Update the affected sections; do not regenerate whole documents.

A feature page, where warranted, covers: purpose; user-visible behavior; business rules and permissions; main flow through the system; relevant code and tests; links to decisions; unsupported cases with links to shortcuts. It must not just list classes and functions.

## 4. Decisions

Record a decision when a later developer would otherwise ask "why not the obvious alternative?", not for routine choices that follow conventions. Record it when it is made; never invent past reasoning, and label inferred or unknown rationale.

```text
Decision:
Context:
Chosen approach:
Alternatives considered:
Consequences:
Status:
```

If the mode creates no files and `decisions.md` does not exist, put the record in the delivery report for the commit or pull request description.

## 5. Shortcuts and limitations

Each deliberate shortcut is a one-line comment at its code site, in the project's comment syntax:

```text
shortcut: <the limit and its consequence>, revisit when <trigger>
```

Search the code for `shortcut:` to list them all. If a shortcut affects users, security, data, or operations (demo-only authentication, a missing backup), also state its consequence in the relevant system document and link to the code. A limitation with no code site, such as an unsupported platform, goes in the README status or the feature page. The delivery report lists the shortcuts this change added.

## 6. `ui.md`: the UI contract

`ui.md` is an active implementation contract. Cover, where applicable: design principles; visual foundations and token references; layout and navigation; shared components and usage; forms and validation; search, filters, pagination; saving and submission; destructive actions and confirmation; loading, empty, error, success, and restricted states; terminology and messages; dates, numbers, currencies, localization; keyboard, focus, accessibility; responsive behavior; intentional exceptions with rationale; representative implementation references.

Sources of truth: tokens and themes hold the actual values; shared components hold reusable appearance and behavior; `ui.md` holds intent, conventions, usage, and exceptions; feature docs hold business meaning; architecture docs hold system boundaries. Link between them; do not duplicate definitions.

## 7. Accuracy

- Ground implementation claims in inspected evidence.
- Keep planned, mocked, incomplete, and implemented behavior apart, and implemented apart from verified.
- Link to authoritative code or schemas instead of copying large definitions.
- Exclude secrets and sensitive records.
- When documentation and code disagree, one is wrong: a code defect or outdated docs. Fix the wrong one in the same change when in scope. If the intended behavior is unclear, ask; never redefine intent to match the code.
- One domain concept keeps one meaning across storage, APIs, logic, UI, messages, and documentation. Document significant intentional differences.

## 8. Five-year return test (`full` only)

The documentation should let a competent developer: explain the purpose; set up and run it; trace one important flow; locate the responsible code; understand significant decisions; find important limitations and shortcuts; find the right checks before changing something. Keep unverified parts of this visible. Delivery reports are not durable documentation.
