# GIT

Rules for commits, branches, and Git hygiene in this project.

## Commits

- Always use **Conventional Commits** format.
- Always write the commit message in **one line**.
- Always write the commit message in **English**.
- NEVER add a `Co-Authored-By:` line. No exceptions.
  Do NOT add `Co-Authored-By: Claude <noreply@anthropic.com>` or any
  variation. The commit must have only the user as author.

### Format

    <type>: <short description>

### Allowed types

- `feat` — A new feature.
- `fix` — A bug fix.
- `chore` — Maintenance, config, setup.
- `docs` — Documentation only.
- `refactor` — Code change that neither fixes a bug nor adds a feature.
- `style` — Formatting, whitespace, no logic change.
- `test` — Adding or modifying tests.
- `perf` — Performance improvement.

### Examples

    feat: add contact form with SMTP integration
    fix: correct typo in footer
    chore: update dependencies
    docs: add git rules
    refactor: extract validation into helper

### Rules

1. Keep the subject under 72 characters.
2. Use imperative mood ("add", not "added" or "adds").
3. Do NOT end the subject with a period.
4. Do NOT add a body unless strictly necessary. One line is the default.

## Branches

- Feature branches use the pattern `feature/<short-kebab-description>`.
- See `CLAUDE.md` → MEMORY PROTOCOL → Branch per feature for the full workflow.
- Never work directly on `main` or `master` for features.

## Co-Authored-By

Never add co-author trailers to commits. The commit must only list
the user as author. This applies to all commits, regardless of how
much the agent contributed.
