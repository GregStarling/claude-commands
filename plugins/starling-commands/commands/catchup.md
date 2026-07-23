Re-orient me in this repo: what happened since it was last touched, what's in flight, and what's next. Read-only — change nothing, commit nothing.

## Gather

Run what applies; skip what the repo doesn't have.

Repo state:

- Current branch, `git status` (uncommitted and untracked work), `git stash list`.
- `git log --oneline -15` for recent history.
- If there's a remote: `git fetch -q`, then `git log --oneline @{u}..HEAD` (unpushed) and `git log --oneline HEAD..@{u}` (unpulled drift).
- If `gh` works here: `gh pr list` for open PRs, `gh run list --limit 5` for recent CI.

Project state (only where these exist):

- `CLAUDE.md` / `ARCHITECTURE.md` for the ground rules if you haven't already loaded them.
- `docs/progress.md` — the most recent entries.
- `docs/prd.json` or similar task tracking — find the next actionable item (lowest incomplete task whose dependencies are done).
- `lessons/` — anything added recently.

## Report — a brief, not a dump

- **Where things stand**: one short paragraph — the last meaningful work, current branch state, anything uncommitted or unpushed.
- **In flight**: open PRs, red CI, stashes, half-done work sitting in the tree (name the files).
- **Next up**: the next task according to the repo's own tracking, or your best inference from the log when there is no tracking.
- **Watch out**: anything broken, drifted, or surprising — failing checks, divergence from remote, status docs that contradict the code.

Keep the whole brief under ~20 lines. Summarize; don't paste raw command output. If the repo is clean, synced, and has nothing in flight, say exactly that in two sentences and stop.
