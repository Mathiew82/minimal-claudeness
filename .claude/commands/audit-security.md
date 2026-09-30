---
description: Run a security audit on recent changes.
---

Launch the `security-auditor` subagent to scan the current changes
for vulnerabilities.

The subagent should:
- Focus on files modified in the working tree or the last commit.
- Look for injection flaws, auth bypasses, sensitive data exposure,
  and insecure configs.
- Report findings with severity, location, risk, and suggested fix.

When it finishes, present its findings to the user in the user's language.
If no issues are found, say so clearly.
