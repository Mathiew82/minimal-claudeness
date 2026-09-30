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

- Do NOT invent content for PROJECT OVERVIEW or STACK.
- Leave those sections as they are (with the `...` placeholders).
- Inform the user in their language:
  "The project looks new or without enough content or context.
   You have the configuration in your hands. You will just need to add
   information about the project in 'PROJECT OVERVIEW' and 'STACK'
   in CLAUDE.md, when you consider it appropriate."

Then skip to Step 4 (do not fill CLAUDE.md or STRUCTURE.md).

If the project HAS meaningful content, proceed to Step 3.

## Step 3 — Fill CLAUDE.md and STRUCTURE.md

### 3a. Fill CLAUDE.md

Edit `CLAUDE.md` and replace the placeholder `...` in these sections:

- **PROJECT OVERVIEW**: 2-4 sentences describing what the project is,
  who it's for, and its main purpose. Be concrete, not generic.
- **STACK**: a clear list of languages, frameworks, versions, and key
  libraries. Use bullet points. Example:
  - Language: TypeScript 5.x
  - Framework: Next.js 14 (App Router)
  - Database: PostgreSQL via Prisma
  - Testing: Vitest + Playwright
  - Package manager: pnpm

Do NOT touch any other section. Do NOT invent information you cannot
verify from the project files.

### 3b. Fill STRUCTURE.md

Rewrite `STRUCTURE.md` with:
- A directory tree (2-3 levels deep, skipping `node_modules`, `.git`, `dist`, `build`, etc.).
- A short description (1 line) of what each main folder/file is for.
- Notes on entry points and key files if identifiable.

Keep it concise. This file is a map, not a book.

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

### 4d. `.claude/personal-instructions.md`

If the file does not exist, create it with:

    # PERSONAL INSTRUCTIONS

    <!--
    Your personal preferences for this project.
    This file is gitignored and never committed.
    Add anything here: coding style, communication preferences,
    local environment notes, reminders for yourself.
    -->

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
- `.claude/personal-instructions.md` — Your personal preferences (not committed). Add anything you want there.
