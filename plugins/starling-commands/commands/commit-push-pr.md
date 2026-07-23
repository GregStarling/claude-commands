---
description: Commit, push, and create a PR for the current changes
---

Commit, push, and create a PR for the current changes.

Here is the current state of the repo:

```bash
git status
```

```bash
git diff --stat
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

1. Review all staged and unstaged changes. If there are unstaged changes that should be included, stage them (prefer specific files over `git add .`).
2. Write a clear, concise commit message that focuses on the "why" not the "what". Follow the repo's existing commit style from the log above.
3. Commit the changes.
4. Push the branch to origin (create the remote branch with `-u` if needed).
5. Create a PR using `gh pr create` with:
   - A short title (under 70 chars)
   - A body with `## Summary` (1-3 bullets) and `## Test plan` sections
6. Return the PR URL.

If there are no changes to commit, say so and stop.
