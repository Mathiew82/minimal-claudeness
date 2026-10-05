---
description: Configure Minimal Claudeness for this project.
---

Configure Minimal Claudeness. Follow these steps EXACTLY.

## Step 0 — Announce

Before doing anything else, tell the user (in their own language):

"⌛ Minimal Claudeness is being configured..."

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

## Step 2 — Detect if the project is empty or minimal

If you find NO manifest files, NO README, NO meaningful source code,
or fewer than ~3 files total (excluding the Minimal Claudeness files
themselves):

Treat the project as **new/empty**. In that case:

- Do NOT invent content for OVERVIEW.md or STACK.md.
- Leave those sections as they are (with the `...` placeholders).
- Inform the user in their language:
  "The project looks new or without enough content or context.
   You have the configuration in your hands. You will just need to add
   information about the project in 'OVERVIEW.md' and 'STACK.md'
   when you consider it appropriate."

Then skip to Step 4 (do not fill CLAUDE.md, STRUCTURE.md, or DESIGN.md).

If the project HAS meaningful content, proceed to Step 3.

## Step 3 — Fill OVERVIEW.md, STACK.md and STRUCTURE.md

### 3a. Fill OVERVIEW.md

Edit `OVERVIEW.md` and replace the placeholder `...` with 2-4 sentences
describing what the project is, who it's for, and its main purpose.
Be concrete, not generic.

### 3b. Fill STACK.md

Edit `STACK.md` and replace the placeholder `...` with a clear list of
languages, frameworks, versions, and key libraries. Use bullet points.
Example:
- Language: TypeScript 5.x
- Framework: Next.js 14 (App Router)
- Database: PostgreSQL via Prisma
- Testing: Vitest + Playwright
- Package manager: pnpm

### 3c. Fill STRUCTURE.md

Rewrite `STRUCTURE.md` with:
- A directory tree (2-3 levels deep, skipping `node_modules`, `.git`, `dist`, `build`, etc.).
- A short description (1 line) of what each main folder/file is for.
- Notes on entry points and key files if identifiable.

Keep it concise. This file is a map, not a book.

Do NOT invent information you cannot verify from the project files.
Do NOT touch `CLAUDE.md`.

### 3d. Fill DESIGN.md

Apply this step ONLY if the project has a user interface (web app, mobile
app, desktop app). If the project is a backend, CLI, library, or has no
UI, skip this step entirely and leave `DESIGN.md` as is.

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

#### Cases

1. **The project has no UI.** Skip this step entirely. `DESIGN.md` is
   left as is.

2. **The project has a UI but no `DESIGN.md`, or it is empty/placeholder.**
   Analyze the existing design system and fill `DESIGN.md` from scratch
   following the spec above.

3. **The project has a UI and an existing `DESIGN.md` with real content.**
   Rewrite `DESIGN.md` to conform to the spec above. Preserve all the
   real design information from the original file (colors, typography,
   spacing, components, rationale). Reorganize and reformat it to match
   the spec. Do NOT lose information.

   Inform the user before rewriting:
   "Your DESIGN.md has been rewritten to follow the Minimal Claudeness
    spec (https://github.com/google-labs-code/design.md). Review it to
    make sure nothing was lost."

   Do NOT ask for permission. Just inform. The harness is the source of
   truth for the format.

## Step 4 — Ensure required files exist

Check the following files and create them if they are missing. Never
overwrite a file that already exists.

### 4a. `harness-verified.json`

If the file does not exist, create it with:

    {
      "verified": false
    }

Do NOT set it to `true` yet. That happens in Step 5.

### 4b. `DESIGN.md`

If the file does not exist, create it with:

    # DESIGN

    <!--
    Add your design system here: colors, typography, spacing, components.
    This file is optional. If you have no design yet, leave it as is.
    -->

### 4c. `STRUCTURE.md`

If the file does not exist (project was empty), create it with:

    # STRUCTURE

    <!--
    This file will be filled automatically when the project has content.
    -->

### 4d. `OVERVIEW.md`

If the file does not exist, create it with:

    # OVERVIEW

    <!--
    Describe what this project is, who it's for, and its main purpose.
    Keep it concise.
    -->

### 4e. `STACK.md`

If the file does not exist, create it with:

    # STACK

    <!--
    List the languages, frameworks, versions, and key libraries.
    Example:
    - Language: TypeScript 5.x
    - Framework: Next.js 14 (App Router)
    - Database: PostgreSQL via Prisma
    -->

### 4f. `.claude/personal-instructions.md`

If the file does not exist, create it with:

    # PERSONAL INSTRUCTIONS

    <!--
    Your personal preferences for this project.
    This file is gitignored and never committed.
    Add anything here: coding style, communication preferences,
    local environment notes, reminders for yourself.
    -->

### 4g. `.claude/custom-instructions.md`

If the file does not exist, create it with:

    # CUSTOM INSTRUCTIONS

    <!--
    Project-specific instructions that don't fit anywhere else.
    Add any rule, convention, or note that the agent should always follow
    in this project. This file is committed and shared with the team.
    -->

### 4h. `.gitignore`

If `.gitignore` does not exist at the project root, create it. Then
ensure the following three lines are present. Add any that are missing.
NEVER remove existing lines.

    .claude/personal-instructions.md
    .claude/settings.local.json
    memory/CHECKLIST.md

## Step 5 — Mark as verified

Edit `harness-verified.json` and set `"verified": true`.

## Step 6 — Inform the user

Print this message in the user's language. Adjust the agent and command
lists to reflect what actually exists in `.claude/agents/` and
`.claude/commands/`.

---

✅ Minimal Claudeness has been configured successfully!

**About the design system:**
You only need to add the design guide in `DESIGN.md`.
If you have one, add it. If you don't have a design, don't worry,
it's not essential.

**Available agents** (invoke them with `@`):
- `@code-reviewer` — Reviews code for bugs and improvements.
- `@security-auditor` — Audits code for vulnerabilities.
- `@qa-engineer` — Runs types, lint, and tests.

**Available commands** (run them with `/`):
- `/setup-harness` — Reconfigure Minimal Claudeness.
- `/find-feature <term>` — Search a feature in memory.
- `/find-feature --all <term>` — Search also in history.
- `/compact-features` — Archive old features.
- `/review-code` — Run the code reviewer.
- `/audit-security` — Run the security auditor.
- `/qa-automation` — Run the QA engineer.

**Other places where you can customize:**
- `.claude/rules/` — Project-specific rules (style, testing, conventions).
- `.claude/custom-instructions.md` — Project-wide custom instructions (committed).
- `.claude/personal-instructions.md` — Your personal preferences (not committed).
