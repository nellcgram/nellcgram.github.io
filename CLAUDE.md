# Notes for Claude

## Vale

- Run Vale on every docs change before pushing: `vale docs` (all alert levels, not only errors).
- Read every finding and report errors, warnings, and suggestions with file and line.
- The CI job "Vale prose lint" fails only on errors. The separate "vale" check shows "skipping" (neutral) when it has warnings or suggestions on changed lines. Open it and read the findings. Never describe it as skipped or ignore it.
- Do not rewrite the author's wording to clear a finding without asking, unless told to fix them.

## Pull requests

- Check all CI results before calling a PR ready, and name any check that failed or is neutral.
- Stage files by explicit path, not `git add -A`, because the working tree can hold uncommitted edits the author has not asked to commit.
