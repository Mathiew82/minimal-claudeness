---
description: Run automated QA checks (types, lint, tests).
---

Launch the `qa-engineer` subagent to verify the current state of the project.

The subagent should:
- Run type checking, linting, and tests.
- Return a concise pass/fail report.

When it finishes, present its report to the user in the user's language.
If it failed, suggest which files or areas need attention based on the
error messages, but do NOT fix anything yourself.
