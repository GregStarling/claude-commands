# claude-commands

Custom slash commands for [Claude Code](https://claude.com/claude-code), packaged as an installable plugin.

## Install

From any Claude Code session:

```
/plugin marketplace add GregStarling/claude-commands
/plugin install starling-commands@starling
```

That's it — the commands are available in every repo and folder. When the repo gets updates, refresh with `/plugin marketplace update starling`.

## Commands

| Command | What it does |
|---|---|
| `/delegate <task>` | CTO-mode orchestration: the session model scopes and writes work orders, Opus agents implement, then the orchestrator reviews the diffs and personally polishes the result to staff-level quality. Grants Workflow/multi-agent permission for the turn. |
| `/repro <bug>` | Disciplined bug fixing: write the failing test that reproduces the bug first, confirm it fails for the right reason, fix the root cause, prove it with the test, then sweep for sibling bugs. Refuses to fix what it can't reproduce. |
| `/ship` | Commit everything, push to main, and chase CI until it's green. Runs local checks first, updates the repo's task/status docs when it has them, and doesn't stop until it ships or it's genuinely blocked. |
| `/catchup` | Read-only re-orientation in a repo: what happened since you last touched it, what's in flight (PRs, CI, stashes, uncommitted work), and what's next. Produces a short brief, not a wall of command output. |
| `/verify` | Verify the current changes work correctly end-to-end. |
| `/simplify` | Review the code just changed for opportunities to simplify. |
| `/commit-push-pr` | Commit, push, and open a PR for the current changes. |

## Notes

- `/delegate` is written for a setup where the session runs a stronger orchestrator model (Fable) and delegates implementation to Opus agents. It still works on other models — it warns and proceeds — but that pairing is the intent.
- `/ship` and `/catchup` look for project-tracking files (`docs/prd.json`, `docs/progress.md`, `lessons/`) and use them when present. Repos without that structure are handled gracefully — the steps just skip.
- Commands are plain markdown in [plugins/starling-commands/commands/](plugins/starling-commands/commands/). PRs welcome; or copy any file into your own `~/.claude/commands/` if you'd rather not install the plugin.
