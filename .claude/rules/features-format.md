# FEATURES FORMAT

Rules for reading and writing the project's feature memory files.

## Files

- `memory/FEATURES.md` — Active memory. Most recent ~100 entries.
- `memory/FEATURES-HISTORY.md` — Archived entries. Only read with `--all`.

## Entry format

Every feature entry must follow this exact format:

    ## YYYY-MM-DD - Short description
    - **Keywords:** keyword1, keyword2, keyword3
    - **Files:** path/to/file1, path/to/file2
    - **Status:** completed | in-progress | deprecated

Example:

    ## 2024-05-10 - Contact page with form
    - **Keywords:** contact, form, smtp, email
    - **Files:** src/pages/Contact.tsx, src/api/mail.ts
    - **Status:** completed

## Rules for adding entries

1. Always append new entries at the END of `memory/FEATURES.md`.
2. Use today's date in `YYYY-MM-DD` format.
3. Keywords must be lowercase, comma-separated, and searchable.
4. Files must be relative paths from the project root.
5. If a feature modifies an existing one, create a NEW entry referencing it.
6. Never delete or edit old entries — only append.
7. When `FEATURES.md` exceeds 100 entries, suggest running `/compact-features`.

## Rules for history

1. `FEATURES-HISTORY.md` is populated ONLY by `/compact-features`.
2. Never edit or delete entries in the history manually.
3. Preserve chronological order (oldest first).
