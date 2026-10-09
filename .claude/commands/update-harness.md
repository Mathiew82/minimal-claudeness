---
description: Update Minimal Claudeness to the latest version.
---

Update Minimal Claudeness. Follow these steps EXACTLY.

## Step 0 — Announce

Before doing anything else, tell the user (in their own language):

"🔄 Checking for Minimal Claudeness updates..."

Then proceed with Step 1.

## Step 1 — Read current version

Read `harness-manifest.json` at the project root.

If the file does not exist, tell the user:

"This project does not have a `harness-manifest.json`. It looks like
Minimal Claudeness was installed manually or with an older version.
I cannot determine the current version. Do you want to reinstall from
scratch instead?"

Wait for the user's answer.

If the user agrees, execute `/setup-harness` and STOP.
If not, STOP without changes.

Store the current version as `CURRENT`.

## Step 2 — Fetch the latest version

Clone the latest version of Minimal Claudeness into a temporary folder:

    git clone --depth 1 https://github.com/Mathiew82/minimal-claudeness.git .mc-update

If the clone fails, report the error and STOP.

Read `.mc-update/harness-manifest.json` and store its version as `LATEST`.

## Step 3 — Compare versions

If `LATEST == CURRENT`:

Report: "Minimal Claudeness is already up to date (vCURRENT)."
Clean up (delete `.mc-update`) and STOP.

If `LATEST != CURRENT`:

Proceed to Step 4.

## Step 4 — Show what will change

List the files that will be updated. These are the files listed in
`harness_files` of the LATEST manifest.

Show the user:

    Update available: vCURRENT → vLATEST

    Files that WILL be updated:
      - CLAUDE.md
      - harness-manifest.json
      - .claude/agents/*.md
      - .claude/commands/*.md
      - .claude/rules/harness/*.md

    Files that will NOT be touched:
      - OVERVIEW.md, STACK.md
      - DESIGN.md, STRUCTURE.md
      - .claude/rules/user/*.md
      - .claude/settings.json, settings.local.json
      - .claude/custom-instructions.md, user-instructions.md
      - memory/FEATURES.md, FEATURES-HISTORY.md, CHECKLIST.md
      - harness-verified.json
      - .gitignore

Ask: "Proceed with the update?"

Wait for the user's answer.

If the user declines, clean up (delete `.mc-update`) and STOP.

## Step 5 — Apply the update

For each file in `harness_files` from the LATEST manifest:

1. Copy the new version from `.mc-update/<file>` to `<file>` in the
   project, overwriting the existing one.
2. If the file does not exist in `.mc-update`, skip it (the manifest
   may list a file that was removed).

Update `harness-manifest.json` at the project root with the new content
from `.mc-update/harness-manifest.json`.

Do NOT touch any file NOT listed in `harness_files`.

## Step 6 — Clean up

Delete the temporary folder:

    rm -rf .mc-update

## Step 7 — Report

Inform the user (in their own language):

    ✅ Minimal Claudeness updated: vCURRENT → vLATEST

    Updated N files.
    Nothing else was touched.

If any file failed to copy, list it in the report.
