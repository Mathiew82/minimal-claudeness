---
description: Archive the oldest features from active memory to history.
---

Manually compact the active memory. Use this when you want to archive
some of the oldest entries to keep the active file lean — even if the
automatic maintenance has not triggered yet.

## Step 1 — Read the counter

Read `memory/FEATURES.md` and locate the line `**Count: N / 100**`.

If `N <= 10`:
Report: "Nothing meaningful to compact. N entries (minimum 10 required)."
STOP.

Otherwise, proceed to Step 2.

## Step 2 — Ask the user

Ask, in the user's language:

"Active memory has N entries. How many of the oldest do you want to
archive to history? (Recommended: keep around 50 active. Example: archive 20)"

Wait for the user's answer.

If the user's number is 0, or greater than or equal to N, ask again
(do not allow archiving all entries or none).

## Step 3 — Move entries

1. Move the specified number of OLDEST entries from `FEATURES.md` to
   the END of `FEATURES-HISTORY.md`, preserving their original order
   (oldest first).
2. Update the `FEATURES-HISTORY.md` counter (`**Count: M**` → `M + K`,
   where K is the number of entries moved).
3. Update the `FEATURES.md` counter (`**Count: N / 100**` → `**Count: N-K / 100**`).
4. Preserve the format of the entries exactly as defined in
   `.claude/rules/features-format.md`. Do not reformat or reword.
5. Report: "Moved K entries to history. Active memory: N-K / 100.
   History: M+K entries."

## Rules

- Never move entries that are less than 7 days old (recent context should
  stay in active memory).
- Never archive all entries. Always leave at least 10 in `FEATURES.md`.
- Do not modify entry content during the move. Byte-for-byte.
