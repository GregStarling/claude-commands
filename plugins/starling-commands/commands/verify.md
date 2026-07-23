---
description: Verify the current changes work correctly end-to-end
---

Verify the current changes work correctly end-to-end.

```bash
git diff HEAD~1 --name-only
```

## Instructions

Based on the files changed:

1. **Identify the right verification strategy**:
   - If there are tests: run them (`cargo test`, `npm test`, `pytest`, etc.)
   - If it's a CLI tool: run it with representative inputs
   - If it's a library: check that it compiles/builds cleanly
   - If it's a web app: build it and check for errors

2. **Run the verification** and report results.

3. **If anything fails**: investigate the root cause, fix it, and re-verify.

4. **Report**: list what was tested and whether it passed.

Do not skip verification. If you're unsure what to test, look at the project's existing test infrastructure (test files, CI config, Makefile/package.json scripts).
