<p align="center">
  <img src=".github/images/logo-min.png" alt="Minimal Claudeness" width="300">
</p>

<h1 align="center">Minimal Claudeness</h1>

<p align="center">
  <em>The essence of working with Claude Code. No dependencies, no noise, no bloat.</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/license-MIT-blue" alt="License">
  <img src="https://img.shields.io/badge/Claude%20Code-ready-purple" alt="Claude Code">
  <img src="https://img.shields.io/badge/dependencies-zero-success" alt="Zero dependencies">
</p>

---

A minimal, dependency-free meta-harness for [Claude Code](https://claude.com/claude-code) that gives your projects **structure, memory, and focused subagents** — the things you actually need, and nothing more.

---

> [!WARNING]
> **Early development.** Minimal Claudeness is still under active development.
> Some features may change, break, or behave unexpectedly. Not recommended
> for production use yet — but feedback, issues, and ideas are very welcome.

---

## Why

Every time you start a new project with Claude, you repeat the same context. Every session, you re-explain the stack. Every feature, you risk duplicating something you already built three months ago.

**Minimal Claudeness fixes that.** One harness, cloned into any project, that bootstraps itself, remembers what you have built, and keeps Claude focused.

No Python. No Node. No SQLite. Just files.

---

## Who is this for

- Solo developers who want structure without ceremony.
- Small teams who need shared context and memory.
- Non-programmers building apps with Claude and tired of repeating themselves.
- Anyone who has ever asked Claude "did we already build this?"

---

## What you get

- 🧠 **Two-tier memory** — A searchable ledger of every feature you have built, with automatic archival when it grows.
- 🌿 **Branch per feature** — Each feature lives on its own branch, keeping `main` clean and the history traceable.
- 📋 **Temporary checklists** — Complex features get a `CHECKLIST.md` that fills the memory as tasks are completed, then disappears.
- 🤖 **Focused subagents** — Code reviewer, security auditor, and QA engineer, invoked only when you ask for them.
- 📐 **Modular rules** — Code style, conventions, and testing live in their own files, loaded on demand.
- 🏗️ **Project structure** — A living map of your project, kept up to date.
- 🎨 **Design system slot** — Drop your design guide in, and Claude respects it.
- 🚀 **Self-configuring** — First session detects it is unconfigured and starts the setup automatically.
- 🔒 **Personal overrides** — Keep your own preferences private, never committed.

---

## Structure

```
your-project/
├── CLAUDE.md                  # Project context and rules (committed)
├── DESIGN.md                  # Design system (committed, optional)
├── STRUCTURE.md               # Project map (committed)
├── harness-verified.json      # Setup state flag
├── CHECKLIST.md               # Temporary, per-feature (gitignored)
├── .gitignore                 # Excludes personal files
├── .claude/
│   ├── settings.json          # Shared permissions (committed)
│   ├── settings.local.json    # Personal permissions (gitignored)
│   ├── personal-instructions.md  # Your preferences (gitignored)
│   ├── agents/
│   │   ├── code-reviewer.md
│   │   ├── security-auditor.md
│   │   └── qa-engineer.md
│   ├── commands/
│   │   ├── setup-harness.md
│   │   ├── find-feature.md
│   │   ├── compact-features.md
│   │   ├── review-code.md
│   │   ├── audit-security.md
│   │   └── qa-automation.md
│   ├── rules/
│   │   ├── code-style.md
│   │   ├── conventions.md
│   │   ├── testing.md
│   │   ├── features-format.md
│   │   └── git.md
│   └── skills/
│       └── personal-instructions/
└── memory/
    ├── FEATURES.md            # Active memory (last ~100 features)
    └── FEATURES-HISTORY.md    # Archived features
```

---

## How to install

### 1. Add Minimal Claudeness to your project

Make sure your project folder already exists before running these commands.
These commands only copy the harness files into your project. Your existing
files (README, LICENSE, .gitignore, etc.) are never overwritten.

**Step 1 — Clone the harness:**

```bash
git clone https://github.com/Mathiew82/minimal-claudeness.git
```

**Step 2 — Copy the harness files into your project:**

<details open>
<summary>Linux / macOS</summary>

```bash
cd minimal-claudeness
rsync -av --exclude='.git' --exclude='README.md' --exclude='LICENSE' --exclude='.github' --exclude='.gitignore' . ../your-project/
cat .gitignore >> ../your-project/.gitignore
cd ..
```
</details>

<details open>
<summary>Windows (PowerShell)</summary>

```powershell
cd minimal-claudeness
$exclude = @('.git', 'README.md', 'LICENSE', '.github', '.gitignore')
Get-ChildItem -Force | Where-Object { $exclude -notcontains $_.Name } | Copy-Item -Destination "..\your-project\" -Recurse -Force
if (-not (Test-Path "..\your-project\.gitignore")) { New-Item -Path "..\your-project\.gitignore" -ItemType File -Force }
Add-Content -Path "..\your-project\.gitignore" -Value (Get-Content ".gitignore")
cd ..
```
</details>

<details open>
<summary>Windows (CMD)</summary>

```cmd
cd minimal-claudeness
xcopy .claude ..\your-project\.claude /E /I /H /Y
xcopy memory ..\your-project\memory /E /I /H /Y
copy CLAUDE.md ..\your-project\
if not exist ..\your-project\.gitignore type nul > ..\your-project\.gitignore
type .gitignore >> ..\your-project\.gitignore
cd ..
```
</details>

**Step 3 — Clean up:**

Once the files are copied, you can safely delete the `minimal-claudeness`
folder — you no longer need it.

```bash
rm -rf minimal-claudeness                               # Linux / macOS
rmdir /S /Q minimal-claudeness                          # Windows (CMD)
Remove-Item -Path "minimal-claudeness" -Recurse -Force  # Windows (PowerShell)
```

**Manual (any OS):**

After Step 1, open the `minimal-claudeness` folder in your file explorer
and drag only these items into your project:

- `.claude/` (folder)
- `memory/` (folder)
- `CLAUDE.md` (file)

Then manually add these three lines to your project's `.gitignore`:

```
.claude/personal-instructions.md
.claude/settings.local.json
CHECKLIST.md
```

### 2. Activate Minimal Claudeness

Once the harness files are in your project, open Claude Code inside it
and send a simple message. Any message works — the harness activates on
your first message. `hi harness` is just a friendly convention.

On the first message, Minimal Claudeness will automatically detect that
it is not configured and start the setup. You will see:

```
⌛ Minimal Claudeness is being configured...
```

Then it will:
- Analyze your project.
- Fill in `PROJECT OVERVIEW` and `STACK` in `CLAUDE.md` (if the project has content).
- Generate `STRUCTURE.md` from your directory tree.
- Create `.claude/personal-instructions.md` for you.
- Ensure your `.gitignore` has the three required lines.
- Mark the harness as verified.
- Show you what is available.

No confirmation needed. Just open Claude Code and say hi.

### 3. Work normally

Before implementing a feature, Claude reads `memory/FEATURES.md` and checks if something similar already exists. If it does, it stops and asks.

For meaningful features, Claude creates a `feature/<short-name>` branch and a temporary `CHECKLIST.md`. As tasks are completed, they are marked in the checklist and summarized into `memory/FEATURES.md`. When the feature is done, the checklist is deleted and the branch is ready for review.

The active memory never exceeds 100 entries. When a new feature would push the count past 100, the oldest entry is automatically moved to `FEATURES-HISTORY.md`.

---

## Commands

| Command | What it does |
|---------|--------------|
| `/setup-harness` | Configures Minimal Claudeness for a new project. |
| `/find-feature <term>` | Searches active memory. |
| `/find-feature --all <term>` | Searches active memory and the archive. |
| `/compact-features` | Archives the oldest entries to history. |
| `/review-code` | Runs the code reviewer subagent. |
| `/audit-security` | Runs the security auditor subagent. |
| `/qa-automation` | Runs the QA engineer subagent. |

---

## Agents

| Agent | Model | When to use |
|-------|-------|-------------|
| `@code-reviewer` | Sonnet | After code changes, before commit. |
| `@security-auditor` | Sonnet | When auth, payments, or user input is involved. |
| `@qa-engineer` | Haiku | When you want types, lint, and tests checked. |

Each agent is **read-only**. None of them modify your files. They report, you decide.

---

## The memory system

Minimal Claudeness uses two files to track what has been built:

**`memory/FEATURES.md`** — Active memory. The most recent ~100 features. Read by Claude before implementing anything new. The file has a counter at the top (`**Count: N / 100**`) that tracks how many entries it contains.

Example entry:

```
## 2024-05-10 - Contact page with form
- **Keywords:** contact, form, smtp, email
- **Files:** src/pages/Contact.tsx, src/api/mail.ts
- **Branch:** feature/contact-form-smtp
```

**`memory/FEATURES-HISTORY.md`** — Archive. Older entries, kept forever, read only when you explicitly ask for it (`/find-feature --all`).

The format is defined in `.claude/rules/features-format.md`.

### Feature workflow

1. **Search** — Claude checks `memory/FEATURES.md` for related work.
2. **Branch** — For meaningful features, Claude creates `feature/<short-name>`.
3. **Checklist** — For complex features, Claude creates a temporary `CHECKLIST.md`.
4. **Implement** — Work happens on the branch, checklist updates as tasks complete.
5. **Record** — Meaningful deliverables are appended to `memory/FEATURES.md` with branch, keywords, and files.
6. **Close** — When done, `CHECKLIST.md` is deleted. The branch is ready for review.

---

## Customization

| File | What to put in it |
|------|-------------------|
| `CLAUDE.md` | Project overview, stack, global conventions. |
| `DESIGN.md` | Your design system (colors, typography, components). |
| `STRUCTURE.md` | A map of your project structure. |
| `.claude/rules/code-style.md` | Formatting, naming, style rules. |
| `.claude/rules/conventions.md` | Commits, branches, patterns. |
| `.claude/rules/testing.md` | Testing framework, structure, commands. |
| `.claude/rules/features-format.md` | Format for memory entries. |
| `.claude/rules/git.md` | Commit format, branch naming, co-author rules. |
| `.claude/personal-instructions.md` | Your personal preferences (gitignored). |

The rules files are empty by default with clear placeholders. Fill them when you need them, not before.

---

## Philosophy

- **Minimal.** If it is not necessary, it is not here.
- **No dependencies.** Pure text, pure Git, pure Claude.
- **Explicit over automatic.** You decide when to invoke agents, not the model.
- **Memory that scales.** Two tiers, archived forever, searchable on demand.
- **Traceable work.** Every feature has a branch, a memory entry, and (if complex) a checklist.
- **Yours.** Personal instructions stay private, project rules stay shared.

> Claude Code is powerful on its own. Minimal Claudeness just gives it a place to think.

---

## Requirements

- [Claude Code](https://claude.com/claude-code)
- Git

That is it.

---

## License

MIT — do whatever you want with it.

---

## Contributing

Found a bug? Have an idea? Open an issue or a PR.

If you build something cool with Minimal Claudeness, I want to hear about it.

---

<p align="center">
  <strong>Minimal Claudeness</strong><br>
  <em>The essence of working with Claude Code.</em>
</p>
