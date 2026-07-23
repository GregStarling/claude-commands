---
description: Reproduce the bug as a failing test before fixing it, then prove the fix with that test
argument-hint: <bug description, error output, or issue link>
---

# /repro — reproduce first, fix second

Bug report: $ARGUMENTS

If nothing was given above, ask for the bug — a description, pasted error output, or an issue link — and stop.

The rule this command enforces: no fix lands without a test that failed because of the bug and passes because of the fix. "Fixed it" and "fixed it and it can't silently come back" are different deliverables; this command produces the second one.

## 1. Understand the report

- If it's an issue or PR link, fetch it. Pull out: expected behavior, actual behavior, and any reproduction steps or stack traces.
- Locate the code path involved and read it. Form a specific hypothesis about the cause before writing anything.

## 2. Write the failing test

- Reproduce the bug at the lowest level that still captures it — a unit test over an integration test over an end-to-end test, whenever the lower level can genuinely exhibit the bug.
- Put it where the repo's existing tests for that area live, matching their style and naming.
- Run it and confirm it fails **for the reported reason**. A test that fails from a setup error, a typo, or a wrong assertion proves nothing — fix the test until its failure message is the bug.
- If you cannot reproduce it after a genuine effort: stop. Report what you tried, what you observed instead, and your best theory for the gap (environment, data, race, already fixed). Do not "fix" a bug you can't observe.

## 3. Fix the root cause

- Fix the cause, not the symptom. If the hypothesis from step 1 turns out wrong, revise it — don't patch around the test.
- Smallest change that fully fixes it. Resist drive-by refactoring; note anything tempting for a follow-up instead.

## 4. Prove it

- The repro test now passes. Run the surrounding suite (and the repo's fast checks — typecheck, lint) to catch regressions.
- Sweep for siblings: does the same bug class exist elsewhere (copy-pasted logic, same misused API)? If yes and cheap, cover and fix those too; if not cheap, list them for follow-up.

## 5. Report

- Root cause, in one or two sentences a teammate would understand.
- The test: file, name, and what it pins down.
- The fix: what changed and why that's the cause and not a symptom.
- Check results, plus any sibling bugs found or follow-ups deferred.

Stop before committing — that's `/ship`'s job when the user wants it.
