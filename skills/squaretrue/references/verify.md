# Verification procedure

## 1. Select checks

Pick the checks that fit the change and its risk, from the tools the project actually has:

- Build or compilation.
- Focused automated tests for the changed behavior.
- Relevant regression tests.
- Runtime or API checks.
- Browser or application interaction.
- UI states, layout, and keyboard operation.
- Security-sensitive behavior (access denied, invalid input, injection paths).
- Focused review of the diff and the code around it.

Use the baseline taken before the first edit to report pre-existing failures separately from failures you introduced. If no baseline was taken, report the origin of a failure as unknown; never infer that it was pre-existing.

## 2. Quality loop

```text
Run checks → Inspect failures → Fix material problems → Recheck
```

- Never weaken, skip, or delete a meaningful test to obtain a pass.
- After two consecutive attempts with the same failure and no new evidence, stop retrying blindly. Continue only with a materially different approach supported by evidence. Otherwise stop with outcome *Blocked* and report the evidence, the remedies tried, and the specific decision or help needed.

## 3. Missing capabilities

If a check cannot be run (no browser, no device, no credentials, no test database), say so in the report. Never imply a UI was observed, or a flow exercised, when it was not.

## 4. Stop when

- The acceptance checks ("Done when") are satisfied.
- Relevant verification is complete, or its gaps are disclosed.
- No known material issue remains within scope.
- Further work would be optional enhancement, not completion.

## 5. Report

List each check that ran with its actual result: the command or method, and pass/fail. List checks not run, and why, under "Limitations / not verified".
