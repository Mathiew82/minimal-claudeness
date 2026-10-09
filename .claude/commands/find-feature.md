---
description: Search the feature memory for an existing implementation.
argument-hint: <term> [--all]
---

Search the feature memory for: "$ARGUMENTS"

## Step 1 — Parse arguments

- Detect if `--all` is present in `$ARGUMENTS`.
- If present, remove it from the search term and set scope to `all`.
- Otherwise, scope is `active`.

The search term is what remains after removing the flag.
If the search term is empty, ask the user what to search for and STOP.

## Step 2 — Read the relevant files

- If scope is `active`: read `memory/FEATURES.md` only.
- If scope is `all`: read both `memory/FEATURES.md` and `memory/FEATURES-HISTORY.md`.

The entry format is defined in `.claude/rules/harness/features-format.md`.
Use it to parse entries correctly.

## Step 3 — Match

Match the search term against:
- The description line (after the date).
- The `Keywords:` field.
- The `Files:` field.

Matching should be case-insensitive and tolerant of partial words.
For example, "contact" should match "contact", "contacts", and "contact-form".

Use `grep` if the files are large. Read directly if they are small.

## Step 4 — Present results

If matches are found, present them in this format (indented as a block):

    📌 Found N matches:

    [YYYY-MM-DD] - [Description]
    Keywords: [keywords]
    Files: [files]
    Location: FEATURES.md | FEATURES-HISTORY.md

Sort results by date, most recent first.

If NO matches are found:

- If scope was `active`:
  "No match in active memory. Try `/find-feature --all $ARGUMENTS` to also search the archived history."
- If scope was `all`:
  "No match anywhere in memory. This appears to be a new feature."

## Step 5 — Ask the user

If matches were found, ask:

"Found N related entries. What would you like to do?
 1. Extend or modify an existing one.
 2. Reuse parts of it for something new.
 3. Create something new anyway.
 4. Just reviewing — nothing to do."

Wait for the user's answer before proceeding.
