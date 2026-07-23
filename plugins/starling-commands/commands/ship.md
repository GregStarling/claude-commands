Commit everything, push to main, and chase CI until it's green. Don't stop until it ships or you're genuinely blocked.

Here is the current state of the repo:

```bash
git status
```

```bash
git diff --stat
```

```bash
git log --oneline origin/main..HEAD
```

```bash
git log --oneline -5
```

```bash
git branch --show-current
```

```bash
git remote -v | head -2
```

## Instructions

### 1. Pre-flight — don't burn CI cycles on failures you can catch locally

- Find the repo's fast checks (package.json scripts, Makefile, CI workflow files) and run them: typecheck, lint, tests, build — whatever exists.
- If anything fails, fix it before committing. CI is for confirmation, not discovery.

### 2. Project bookkeeping — ship the paperwork with the code

- If the repo tracks work in control-plane docs (`docs/prd.json`, `docs/progress.md`, or similar task/status files), bring them up to date with what's shipping: mark finished tasks done, append a progress entry saying what changed and why.
- If the work surfaced a mistake or surprise worth keeping, record it where the repo keeps those (`lessons/` in repos that have it). If the same lesson keeps recurring, say it should graduate into a rule or lint guard instead of another note.
- These updates go in the same commit as the code they describe — a shipped change with stale status docs is half-shipped.
- Repos without any of this structure: skip, don't invent it.

### 3. Squash + commit

- Stage all intended changes (prefer specific files over `git add .`; never stage secrets, local settings, or generated output).
- If there are multiple unpushed local commits (see `origin/main..HEAD` above), squash them into one: `git reset --soft origin/main`, then commit once.
- Write one clear commit message covering the whole change — "why" over "what", matching the repo's existing style from the log above.

### 4. Push to main

- If not on main, confirm with the user before proceeding — shipping a feature branch straight to main is a decision, not a default.
- `git pull --rebase origin main` first to absorb any remote drift; resolve conflicts if trivial, stop and ask if they're substantive.
- Push. If the remote rejects the push (protected branch requiring PRs), say so and fall back to offering a PR instead of fighting it.

### 5. Chase until green

- Check whether the repo has CI (`gh run list --limit 1` or workflow files under `.github/workflows/`). If there is no CI, verify the build locally, report, and stop — that's green.
- Watch the run triggered by your push: `gh run watch <run-id> --exit-status` (get the id from `gh run list --branch main --limit 1`).
- **On failure**: pull the actual error with `gh run view <run-id> --log-failed`. Diagnose the root cause — do not retry a run hoping for flakes unless the log clearly shows an infra/flake failure (in that case, `gh run rerun <run-id> --failed` once).
- Fix the cause locally, re-run the relevant local check to confirm the fix, commit (a normal follow-up commit — don't rewrite history that's already pushed), push, and watch the new run.
- Repeat up to 4 fix attempts. If still red after that, stop and report what's failing, what you tried, and your best theory — don't thrash.

### 6. Report

- Final commit SHA(s) and one-line summary of what shipped.
- CI run URL and its status.
- Anything you fixed along the way to get to green.

If there are no changes to commit and nothing unpushed, say so and stop.
