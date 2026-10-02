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

This workflow applies to EVERY change, regardless of size — a one-line
fix, a copy edit, or a full feature. The feature/small-change distinction
in `CLAUDE.md` → MEMORY PROTOCOL only affects branching and memory
entries, it never changes this step.

1. Before suggesting a commit (steps 2 and 3 below), if the work added,
   removed, or moved files or folders, check that `STRUCTURE.md` reflects
   it, following the criteria in `CLAUDE.md` → ARCHITECTURE. If it does
   not, update it first.

2. Whenever you finish a task — including small fixes, copy edits, or
   config tweaks, not just features — ask the user whether they want to
   commit and push the changes. Do not commit or push until they confirm.
   Never skip this step because the change was small.

3. When a feature (developed on its own `feat/<...>` branch) is finished,
   combine everything into a single question. Ask the user:

   "Do you want me to commit, push, merge the feature branch into `main`,
    and delete the feature branch (local and remote)?"

   Default to doing all four if the user simply confirms. If the user
   asks for a subset (e.g. merge but not delete the branch, or vice
   versa), follow exactly what they request. Do none of it until they
   respond.
