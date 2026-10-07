---
description: Fill or refresh project documentation (OVERVIEW, STACK, STRUCTURE, DESIGN).
---

Fill or refresh the project's documentation files. Follow these steps
EXACTLY.

## Step 0 — Announce

Before doing anything else, tell the user (in their own language):

"📝 Documenting the project..."

Then proceed with Step 1.

## Step 1 — Analyze the project

Scan the project root and key files to understand what this project is.

Look for and read:
- `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `composer.json`, `Gemfile`, or any other manifest.
- `README.md` if it exists.
- The directory tree (top 2-3 levels) to understand structure.
- Config files: `tsconfig.json`, `.eslintrc`, `vite.config.*`, `next.config.*`, `docker-compose.yml`, etc.
- Any existing documentation files.

Determine:
- What the project is (purpose, domain, target users).
- The stack: languages, frameworks, versions, key libraries.
- The architecture: main folders, their responsibilities, entry points.
- Whether the project has a user interface.

## Step 2 — Detect if the project is empty or minimal

If you find NO manifest files, NO README, NO meaningful source code,
or fewer than ~3 files total (excluding the Minimal Claudeness files
themselves):

Inform the user in their language:

"The project still looks empty or without enough content to document.
Nothing has been changed. Come back when the project has some code."

STOP.

If the project HAS meaningful content, proceed to Step 3.

## Step 3 — Fill OVERVIEW.md

Edit `OVERVIEW.md` and replace the placeholder `...` with 2-4 sentences
describing what the project is, who it's for, and its main purpose.
Be concrete, not generic.

If `OVERVIEW.md` already has real content (not a placeholder), ask the
user: "OVERVIEW.md already has content. Do you want me to overwrite it?"

Wait for the user's answer before proceeding.

## Step 4 — Fill STACK.md

Edit `STACK.md` and replace the placeholder `...` with a clear list of
languages, frameworks, versions, and key libraries. Use bullet points.

If `STACK.md` already has real content, ask the user: "STACK.md already
has content. Do you want me to overwrite it?"

Wait for the user's answer before proceeding.

## Step 5 — Fill STRUCTURE.md

Rewrite `STRUCTURE.md` with:
- A directory tree (2-3 levels deep, skipping `node_modules`, `.git`, `dist`, `build`, etc.).
- A short description (1 line) of what each main folder/file is for.
- Notes on entry points and key files if identifiable.

This file is regenerated every time. No need to ask for confirmation.

## Step 6 — Fill DESIGN.md

Apply this step ONLY if the project has a user interface (web app, mobile
app, desktop app). If the project is a backend, CLI, library, or has no
UI, skip this step entirely.

DESIGN.md follows the format spec from
https://github.com/google-labs-code/design.md. The output must use:
- YAML front matter with `colors`, `typography`, `rounded`, `spacing`,
  and `components` tokens.
- Markdown body with sections in this order: Overview, Colors,
  Typography, Layout, Elevation & Depth, Shapes, Components,
  Do's and Don'ts.

Extract tokens from whatever the project uses: CSS variables, Tailwind
config, theme files, styled-components, design tokens JSON, or inline
styles. Do NOT invent values. Only document what exists.

If `DESIGN.md` already has real content (not a placeholder), ask the
user: "DESIGN.md already has content. Do you want me to overwrite it?"

Wait for the user's answer before proceeding.

## Step 7 — Report

Inform the user (in their own language):

"✅ Project documentation updated:
 - OVERVIEW.md
 - STACK.md
 - STRUCTURE.md
 - DESIGN.md (if applicable)

Nothing else was touched."
