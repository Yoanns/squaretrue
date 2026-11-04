---
name: squaretrue
description: Development workflow for coding tasks (understand, shape, build, verify, document, deliver) with risk-based interruptions, evidence-backed results, and maintained documentation. Use when the project's agent instruction file has a "Squaretrue" section, or when the user asks to use Squaretrue for a task. Do not activate merely because this skill is installed.
---

# Squaretrue

> Build quickly. Build coherently. Keep the knowledge.

Central rule: **move quickly on reversible decisions; slow down at trust boundaries, irreversible actions, and expensive commitments.**

## Activation and settings

Activate only when the project's agent instruction file contains a `Squaretrue` section, or the user asks to use Squaretrue for this task. Read the section for:

- **Documentation:** `existing-only` | `full` | `report-only`
- **Action policy:** restrictions and preferences (it never grants permission)
- **Handoff location:** default `HANDOFF.md`
- Links to project guidance packs, if any

No `Squaretrue` section (including single-task use): use `report-only`, no action policy, and do not commit a handoff.

The documentation mode decides every documentation write in this workflow: `report-only` writes no documentation files; `existing-only` writes only into files that already exist; `full` maintains the structure in [document.md](references/document.md). Anything not written goes in the delivery report.

## References: load only when needed

| When | Load |
|---|---|
| Every task, before building | [quality.md](references/quality.md): quality contract and authorization boundary |
| Before verifying | [verify.md](references/verify.md) |
| Before documenting | [document.md](references/document.md) |
| The change touches UI, API, database, native/desktop, or infrastructure | The matching section of [domains.md](references/domains.md) |
| The project uses an ecosystem with a pack | That pack. Project packs linked from the `Squaretrue` section take precedence over the [examples](references/packs/README.md) |

Project-specific rules take precedence over references and packs.

## Questions and updates

| Situation | Do |
|---|---|
| The repository can answer it | Inspect instead of asking |
| Low-risk, reversible choice | Pick a sensible default; disclose it when relevant |
| Several minor unknowns | Group them as assumptions; do not ask one at a time |
| Ambiguity materially changes the behavior | Ask one focused question, with a recommendation |
| Sensitive data, access control, destructive operations, production, substantial cost | Pause for the decision or authorization |
| Request conflicts with repository policy | Keep the policy; explain the conflict |
| Host-specific permission needed | Use the host's permission mechanism |

There is no question limit that would justify unsafe guessing. Progress updates report milestones, material discoveries, or blockers, not each tool operation.

## Workflow

```text
Understand → Shape → Build → Verify → Document → Deliver
                       ↑         |         |
                       └─────────┴─────────┘
                         Correct material gaps
```

The stages are responsibilities within one continuous workflow, not approval gates.

### 1. Understand

Read the project instructions. Inspect the relevant code, tests, configuration, and docs. Find a representative existing implementation. Establish the project's languages, frameworks, conventions, and real build/test commands, and its exposed interfaces. Before the first edit, run the proportionate checks you will use to verify the change, when feasible, and note which already fail. Identify the sensitive boundaries this change touches.

Produce the working agreement, and open with it as a brief orientation:

```text
Goal:          What useful outcome will be delivered?
Done when:     Observable acceptance checks.
Not included:  Explicit scope boundaries.
Assumptions:   Only material assumptions needed to proceed.
```

The orientation is informational unless approval is genuinely required. It must state "Done when" and "Not included" so the user can correct them. For small tasks it stays in the conversation.

In an under-documented project, do not block a small change to document the whole repository: explain the affected area and record the broader gaps (as the documentation mode allows).

### 2. Shape

Choose the smallest understandable solution. Name the affected components and interfaces, the verification methods, the documentation and UI impact, and any decision that needs the user. Output a few-step outline. Routine changes proceed without pausing; complex or consequential ones may need a focused planning discussion.

Add no dependency, abstraction, or infrastructure without a concrete need.

### 3. Build

- Implement a slice that proves something useful. Mock data must be clearly identified; a persistence feature includes its storage behavior; a backend feature needs no UI; never present a mocked integration as working.
- Reuse established patterns, components, and dependencies.
- Add validation, error handling, access restrictions, and tests alongside the behavior ([quality.md](references/quality.md)).
- Stay in scope: no unrelated cleanup or speculative refactoring unless the request needs it to be safe.
- Comment only the reasoning the code cannot show. Mark each deliberate shortcut at its code site: `shortcut: <the limit and its consequence>, revisit when <trigger>`.
- Preserve user changes and existing safeguards.

### 4. Verify

Follow [verify.md](references/verify.md): run checks, inspect failures, fix material problems, recheck. Never weaken meaningful tests to get a pass. After two consecutive attempts with the same failure and no new evidence, change approach based on evidence or stop and report.

### 5. Document

Follow [document.md](references/document.md). Describe what exists, not what was planned. If no developer-facing explanation changes, report `Documentation impact reviewed: no update needed.`

### 6. Deliver

```text
Outcome
- Exactly one: Verified | Implemented, partly verified | Blocked | Investigated

Built
- Delivered behavior.

Verified
- Checks executed and their actual results (pre-existing failures listed separately).

Documentation
- Updated documents, or why no update was needed; gaps and records not written
  because of the documentation mode.

Limitations / not verified
- Shortcuts added (shortcut: comments), gaps, remaining uncertainty.

Decision needed
- Only when a specific unresolved decision exists.
```

Delivery does not authorize deployment, publishing, merging, or any other consequential action.

## Outcomes and definition of done

State **Verified** or **Implemented, partly verified** only when:

- The agreed behavior is implemented, within scope, with safeguards preserved.
- Verification results and gaps are explicit; no known material blocker is undisclosed.
- UI and system conventions are followed.
- Affected developer documentation is current, as the documentation mode requires.
- Significant decisions are recorded and deliberate shortcuts are marked in code.
- Project governance is respected, and the report matches the evidence.

| Outcome | Meaning |
|---|---|
| Verified | Agreed behavior implemented and the required checks passed |
| Implemented, partly verified | Implementation exists; some required checks not performed or not passed |
| Blocked | A decision, permission, dependency, or unresolved failure prevents progress |
| Investigated | Findings delivered, no implementation claim |

Only *Verified* is fully verified completion.

## Session handoff

Only when unfinished work or context warrants it, write a handoff at the configured location (default `HANDOFF.md`):

```text
Goal
Current state
Important decisions
Known limitations
Checks completed
Next action
```

Commit it only in a project with a `Squaretrue` section, and only where its action policy and your permissions allow committing. Delete it when the work is complete. Never overwrite or delete a handoff this task did not create. A handoff does not replace system documentation.
