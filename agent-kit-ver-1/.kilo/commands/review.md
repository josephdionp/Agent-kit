Review the changes. Review only — don't fix anything unless I ask.

1. Run `git status` first. If uncommitted edits are still changing in a way
   that affects the review, tell me to pause and review only the committed or
   explicitly requested diff.
2. Read the full diff plus enough surrounding code to judge it in context —
   don't review changed lines in isolation.
3. Findings first, ordered by severity, each with a `file:line` reference.
   Focus on: bugs, regressions, security issues, broken contracts, missing
   tests, production risks.
4. Skip style nits the linter would catch.
5. No findings → say so plainly, and name any residual verification gaps
   (things you couldn't check).
