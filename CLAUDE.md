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

# ARCHITECTURE

Project structure is documented in `STRUCTURE.md`.
The design system and UI conventions live in `DESIGN.md`.

## Keeping STRUCTURE.md up to date

STRUCTURE.md is a map of the project. Update it, silently and as part of
the same task, whenever you:
- create, delete, rename, or move a folder;
- add a new top-level module, route group, plugin, store, or entry point;
- change what a folder is responsible for.

Do NOT update it for extra files inside a folder whose entry already
covers them (e.g. one more component inside `components/`).

"Silently" means without asking the user. It does not mean optional.

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
- `git.md` — Commit format, branch naming, co-author rules.

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

Use the pattern: `feat/<short-kebab-description>`

Examples:
- `feat/contact-form-smtp`
- `feat/user-authentication`
- `feat/payment-stripe`
- `feat/past-perfect-translations`

Keep it short, lowercase, hyphenated. No spaces, no uppercase, no underscores.

### Workflow

1. Before implementing a feature:
   - If currently on `main` or `master`, create the branch:
     `git checkout -b feat/<short-kebab-description>`
   - If already on a feature branch for the SAME feature, continue there.
   - If on a different feature branch, ask the user before switching.
2. Implement the feature on that branch.
3. After implementing, register the entry in `memory/FEATURES.md`.
4. Do NOT commit, push, or merge. See `.claude/rules/git.md` for the
   commit and push workflow.

### Exception

Small changes (as defined in "What counts as a feature") do NOT
require a branch. Keep working on the current branch.

## Feature checklist

When starting a feature that has multiple steps or sub-tasks, create a
temporary `CHECKLIST.md` file at the project root to track progress.

### When to create a checklist

Create a `CHECKLIST.md` when:
- The feature involves more than 3-4 distinct implementation steps.
- The feature spans multiple files or modules.
- The feature has dependencies or sequential steps.

Do NOT create a checklist for small features that can be done in one pass.

### Checklist format

The checklist must follow this exact format:

    # CHECKLIST — <feature short description>

    Branch: feat/<short-kebab-description>
    Started: YYYY-MM-DD

    ## Tasks

    - [ ] Task 1 description
    - [ ] Task 2 description
    - [ ] Task 3 description

    ## Notes

    <!-- Add relevant notes here as you work -->

### Workflow

1. Create `CHECKLIST.md` at the project root before starting the work.
2. As each task is completed:
   - Mark it as done in `CHECKLIST.md` (`- [x]`).
   - If the task represents a meaningful, searchable deliverable
     (e.g., a new endpoint, a new component, a new service), append a
     sub-entry to `memory/FEATURES.md` following the format in
     `.claude/rules/features-format.md`.
   - Do NOT register trivial sub-tasks (e.g., "renamed a file",
     "added a helper function").
3. When ALL tasks are done:
   - Append a final summary entry to `memory/FEATURES.md` for the feature.
   - Delete `CHECKLIST.md`.
   - Inform the user that the feature is complete and the checklist was removed.

### Rules

- Only ONE `CHECKLIST.md` exists at a time. There is one per active feature.
- If the user asks to work on a different feature while a checklist exists,
  ask them whether to finish the current one first or abandon it.
- `CHECKLIST.md` is never committed. It is listed in `.gitignore`.

## After implementing a feature

1. If the feature added, removed, or moved files or folders, compare the
   project tree with STRUCTURE.md and update it (see ARCHITECTURE).
2. Append a new entry at the END of `memory/FEATURES.md`.
3. Follow the format defined in `.claude/rules/features-format.md`.
4. Use today's date in `YYYY-MM-DD` format.
5. Include description, keywords, and files.
6. Update the counter at the top of `FEATURES.md` (`**Count: N / 100**`).
   If the count was already at 100 before appending, first move the
   oldest entry to `FEATURES-HISTORY.md` (see Maintenance section).
7. Never delete or edit old entries — only append.

## When to consult the history

`FEATURES-HISTORY.md` should NOT be read by default — it can be large.
Only read it when:
- The user explicitly runs `/find-feature --all <term>`.
- The user asks about historical work ("did we ever implement X?").
- You suspect something was built long ago and cannot find it in active memory.

## Maintenance

`memory/FEATURES.md` has a counter at the top: `**Count: N / 100**`.

### When appending a new entry

1. Read the counter in `FEATURES.md`.
2. If `N < 100`:
   - Append the new entry.
   - Update the counter to `N + 1`.
3. If `N == 100`:
   - Move the OLDEST entry from `FEATURES.md` to the END of
     `FEATURES-HISTORY.md`.
   - Update the history counter (`**Count: M**` → `M + 1`).
   - Append the new entry to `FEATURES.md`.
   - Keep the counter at `100 / 100`.

Never let `FEATURES.md` exceed 100 entries. The counter must always
reflect the real number of entries below.

### Manual compaction

The user can still run `/compact-features` at any time to force a
bulk archive (e.g., moving the oldest 20 at once). This is optional;
the automatic rule above keeps the memory healthy without manual work.

## Available commands

- `/find-feature <term>` — Search active memory only.
- `/find-feature --all <term>` — Search active memory and history.
- `/compact-features` — Archive oldest entries from active memory to history.

# PROJECT CONTEXT

@OVERVIEW.md
@STACK.md

# PROJECT CUSTOM INSTRUCTIONS

@.claude/custom-instructions.md

# PERSONAL INSTRUCTIONS

@.claude/personal-instructions.md
