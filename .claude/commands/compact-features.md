---
description: Archive the oldest features from active memory to history.
---

Compact the active feature memory. Follow these steps EXACTLY.

## Step 1 — Read and count

1. Read `memory/FEATURES.md`.
2. Count the feature entries.
   An entry starts with a line matching `## YYYY-MM-DD - ...`.
   Ignore the header and HTML comments.
3. Remember the total count as N.

## Step 2 — Decide

- If N ≤ 100:
  Report: "No compaction needed. Currently N features (minimum 100 required)."
  STOP.

- If N > 100:
  Proceed to Step 3.

## Step 3 — Split

1. Identify the **100 most recent** entries (the last 100 in the file).
2. Identify the **older** entries (everything before those 100).
3. Remember how many older entries there are as M.

## Step 4 — Append older entries to history

1. If `memory/FEATURES-HISTORY.md` does not exist, create it with this exact content (indented as a block):

    # FEATURES HISTORY

    Archived features compacted from `FEATURES.md`.
    Entries are appended here in chronological order, oldest first.

    <!-- Compacted entries will be appended below this line. -->

2. Append the older entries to the END of `memory/FEATURES-HISTORY.md`, preserving their original order (oldest first).
3. Keep the exact entry format defined in `.claude/rules/features-format.md`. Do not reformat or reword entries.

## Step 5 — Rewrite FEATURES.md

Rewrite `memory/FEATURES.md` so it contains ONLY:

1. The file header (the first block of text before the first entry).
2. The 100 most recent entries, in their original order.
3. The final comment line: `<!-- Add new entries below this line. -->`

Do NOT keep any HTML format comments in `FEATURES.md`.
The format lives in `.claude/rules/features-format.md`.

## Step 6 — Report

Inform the user:

"Compaction complete.
 - Moved M entries to `FEATURES-HISTORY.md`.
 - Kept 100 entries in `FEATURES.md`.
 - Total archived so far: [count lines in history]."

Then suggest: "You can commit the changes now."
