---
description: Run a full code review on recent changes.
---

Launch the `code-reviewer` subagent to review the current changes.

The subagent should:
- Focus on files modified in the working tree or the last commit.
- Follow the rules in `.claude/rules/harness/code-style.md`,
  `.claude/rules/user/code-style.md`, and
  `.claude/rules/user/conventions.md`.
- Report issues grouped by severity (Critical, Warning, Suggestion).

When it finishes, present its findings to the user in the user's language.
Group results by severity, most critical first.
