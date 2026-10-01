# FEATURES FORMAT

Rules for reading and writing the project's feature memory files.

## Files

- `memory/FEATURES.md` — Active memory. Has a `**Count: N / 100**` counter
  at the top. Read most recent ~100 entries.
- `memory/FEATURES-HISTORY.md` — Archived entries. Has a `**Count: N**`
  counter at the top. Only read with `--all`.

## Entry format

Every feature entry must follow this exact format:

    ## YYYY-MM-DD - Short description
    - **Keywords:** keyword1, keyword2, keyword3
    - **Files:** path/to/file1, path/to/file2

Example:

    ## 2024-05-10 - Contact page with form
    - **Keywords:** contact, form, smtp, email
    - **Files:** src/pages/Contact.tsx, src/api/mail.ts

## Rules for adding entries

1. Always append new entries at the END of `memory/FEATURES.md`.
2. Use today's date in `YYYY-MM-DD` format.
3. Keywords must be lowercase, comma-separated, and searchable.
4. Files must be relative paths from the project root.
5. If a feature modifies an existing one, create a NEW entry referencing it.
6. Never delete or edit old entries — only append.
7. Update the counter at the top of the file after appending.

## Rules for history

1. `FEATURES-HISTORY.md` is populated by the automatic maintenance rule
   (see `CLAUDE.md` → MEMORY PROTOCOL → Maintenance) or by the
   `/compact-features` command.
2. Never edit or delete entries in the history manually.
3. Preserve chronological order (oldest first).
4. Update the counter at the top of the history file after appending.
