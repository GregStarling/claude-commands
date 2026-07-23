Review the code I just changed for opportunities to simplify.

```bash
git diff HEAD~1 --name-only
```

```bash
git diff HEAD~1
```

## Instructions

Review the changed code above and look for:

1. **Dead code**: Unused variables, unreachable branches, unnecessary imports
2. **Duplication**: Repeated logic that could be consolidated
3. **Over-engineering**: Abstractions that aren't needed yet, unnecessary indirection
4. **Simplification**: Complex expressions that could be clearer, verbose patterns that have simpler alternatives

For each issue found, fix it directly. Do NOT add comments, docstrings, or type annotations that weren't there before. Keep changes minimal — only simplify, don't refactor or add features.

If the code is already clean, say so.
