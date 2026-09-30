# ⚠️ BOOTSTRAP CHECK — READ THIS FIRST

**DO NOT RESPOND TO THE USER UNTIL YOU COMPLETE THIS CHECK.**

Before answering anything, before processing any request, before reading
any other section of this file:

1. Check if `harness-verified.json` exists at the project root.
2. If the file does NOT exist, OR if `verified` is `false`:
   - STOP. Do not process the user's request yet.
   - Execute `/setup-harness` immediately.
   - Do not ask the user for permission. Do not wait for confirmation.
   - After the setup finishes, continue with the user's original request.
3. If `verified` is `true`: continue with the user's request normally.

This check takes priority over everything else in this file.

# PROJECT OVERVIEW

...

# STACK

...

# ARCHITECTURE

Project structure is documented in `STRUCTURE.md`.
The design system and UI conventions live in `DESIGN.md`.

Keep `STRUCTURE.md` updated when the project structure changes
(new folders, new modules, reorganizations). Update it silently as
part of your normal workflow — no need to ask the user.

# GLOBAL CONVENTIONS

- Always respond in the user's language. If the user writes in Spanish,
  respond in Spanish. If in English, respond in English.
- Code, variable names, commits, and file contents must always be in English.

# PROJECT RULES

Detailed project rules live in `.claude/rules/`:

- `code-style.md` — Formatting, naming, and style rules.
- `conventions.md` — Project-wide conventions (commits, branches, patterns).
- `testing.md` — Testing framework, structure, and commands.
- `features-format.md` — Format for memory entries.

Read the relevant file when working on tasks that touch those areas.
If a file is empty, do not assume rules that are not written there.

# MEMORY PROTOCOL

This project uses a two-tier memory system to track implemented features
and prevent duplicating work across sessions.

## Files

- `memory/FEATURES.md` — Active memory. Most recent ~100 features.
- `memory/FEATURES-HISTORY.md` — Archived features. Only read on demand.

The exact entry format is defined in `.claude/rules/features-format.md`.
Always follow that format when reading or writing entries.

## What counts as a "feature"

A feature is a **meaningful unit of functionality** that adds or changes
behavior in a way that could reasonably be searched for later.

**Consult the memory when the request is:**
- A new form, page, section, or module.
- A new service, API integration, or data flow.
- A new business rule, validation, or workflow.
- A significant refactor that changes how something works.

**Do NOT consult the memory when the request is:**
- A trivial UI change (styling, colors, spacing, moving elements).
- A typo fix, copy edit, or text change.
- Adding or modifying a single button, icon, or label.
- Dependency updates or configuration tweaks.
- Small bug fixes that do not change functionality.

When in doubt, ask the user: "Is this a new feature, or a small change?"

## Before implementing a feature

1. Read `memory/FEATURES.md`.
2. Search for keywords related to the user's request.
3. If a similar or related feature exists:
   - STOP.
   - Tell the user what you found (date, description, files, status).
   - Ask whether to extend/modify it, reuse it, or create something new.
4. If nothing similar exists, proceed with the branch and implementation
   steps described below.

For older work not in active memory, the user can run
`/find-feature --all <term>` to also search `FEATURES-HISTORY.md`.

## Branch per feature

Every feature (as defined above — not trivial changes) must be developed
on its own dedicated branch. Do NOT work on the main branch directly.

### Naming convention

Use the pattern: `feature/<short-kebab-description>`

Examples:
- `feature/contact-form-smtp`
- `feature/user-authentication`
- `feature/payment-stripe`
- `feature/admin-dashboard`

Keep it short, lowercase, hyphenated. No spaces, no uppercase, no underscores.

### Workflow

1. Before implementing a feature:
   - If currently on `main` or `master`, create the branch:
     `git checkout -b feature/<short-kebab-description>`
   - If already on a feature branch for the SAME feature, continue there.
   - If on a different feature branch, ask the user before switching.
2. Implement the feature on that branch.
3. After implementing, register the entry in `memory/FEATURES.md`
   (including the branch name in the entry — see format rules).
4. Do NOT push. Let the user decide when to push and open a PR.

### Exception

Small changes (as defined in "What counts as a feature") do NOT
require a branch. Keep working on the current branch.

## After implementing a feature

1. Append a new entry at the END of `memory/FEATURES.md`.
2. Follow the format defined in `.claude/rules/features-format.md`.
3. Use today's date in `YYYY-MM-DD` format.
4. Include description, keywords, files, branch, and status.
5. Never delete or edit old entries — only append.

## When to consult the history

`FEATURES-HISTORY.md` should NOT be read by default — it can be large.
Only read it when:
- The user explicitly runs `/find-feature --all <term>`.
- The user asks about historical work ("did we ever implement X?").
- You suspect something was built long ago and cannot find it in active memory.

## Maintenance

- When `memory/FEATURES.md` exceeds 100 entries, suggest running
  `/compact-features` to archive the oldest entries to `FEATURES-HISTORY.md`.
- Never trigger compaction automatically. Always ask the user first.

## Available commands

- `/find-feature <term>` — Search active memory only.
- `/find-feature --all <term>` — Search active memory and history.
- `/compact-features` — Archive oldest entries from active memory to history.

# PERSONAL INSTRUCTIONS
@.claude/personal-instructions.md
