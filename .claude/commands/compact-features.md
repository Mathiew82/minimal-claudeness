---
description: Archive the oldest features from active memory to history.
---

Manually compact the active memory. Use this when you want to move
several old entries to history at once.

## Step 1 — Read the counter

Read `memory/FEATURES.md` and locate the line `**Count: N / 100**`.

If `N <= 100`: report "Nothing to compact. N entries (max 100)." and STOP.

If `N > 100` (should not happen with automatic maintenance, but just in case):
proceed to Step 2.

## Step 2 — Ask the user

Ask: "Active memory has N entries. How many of the oldest do you want to
archive? (e.g., 20)"

Wait for the user's answer.

## Step 3 — Move entries

1. Move the specified number of oldest entries from `FEATURES.md` to
   the END of `FEATURES-HISTORY.md`.
2. Update the history counter.
3. Update the `FEATURES.md` counter.
4. Report: "Moved M entries. Active memory: N-M / 100. History: P entries."
