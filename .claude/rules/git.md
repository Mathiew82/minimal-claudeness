# GIT

Rules for commits, branches, and Git hygiene in this project.

## Commits

Always use **Conventional Commits** format, in **one line**, in **English**.

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

## Co-Authored-By

**NEVER** add a `Co-Authored-By:` trailer to any commit. No exceptions.

Do NOT add `Co-Authored-By: Claude <noreply@anthropic.com>`, or any other
variation, regardless of how much the agent contributed. The commit must
list only the user as author.

## Branches

See `CLAUDE.md` → MEMORY PROTOCOL → Branch per feature.

Naming pattern: `feat/<short-kebab-description>`

Examples:
- `feat/contact-form-smtp`
- `feat/user-authentication`
- `feat/past-perfect-translations`

## Commit and push workflow

1. Before suggesting a commit (steps 2 and 3 below), if the work added,
   removed, or moved files or folders, check that STRUCTURE.md reflects
   it, following the criteria in `CLAUDE.md` → ARCHITECTURE. If it does
   not, update it first.
2. Whenever you finish a task, ask the user whether they want to commit
   and push the changes. Do not commit or push until they confirm.
3. When a feature is finished, suggest to the user: commit, push, merge
   the feature branch into `main`, and delete the feature branch (local
   and remote) so no dead branches are left behind. Do none of it until
   they confirm.
