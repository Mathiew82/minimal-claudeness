<p align="center">
  <img src=".github/images/logo-min.png" alt="Minimal Claudeness" width="300">
</p>

<h1 align="center">Minimal Claudeness</h1>

<p align="center">
  <em>The essence of working with Claude Code. No dependencies, no noise, no bloat.</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/license-MIT-blue" alt="License">
  <img src="https://img.shields.io/badge/Claude%20Code-ready-slateblue" alt="Claude Code">
  <img src="https://img.shields.io/badge/dependencies-zero-darkorchid" alt="Zero dependencies">
</p>

<p align="center">
  <a href="#-how-to-install"><strong>Install</strong></a> ·
  <a href="#-how-to-update"><strong>Update</strong></a> ·
  <a href="#-commands"><strong>Commands</strong></a> ·
  <a href="#-agents"><strong>Agents</strong></a> ·
  <a href="#-the-memory-system"><strong>Memory</strong></a> ·
  <a href="#%EF%B8%8F-how-it-works"><strong>How it works</strong></a>
</p>

---

A minimal, dependency-free meta-harness for [Claude Code](https://claude.com/claude-code) that gives your projects **structure, memory, and focused subagents** — the things you actually need, and nothing more.

---

## 🎯 Why

Every time you start a new project with Claude, you repeat the same context. Every session, you re-explain the stack. Every feature, you risk duplicating something you already built three months ago.

**Minimal Claudeness fixes that.** One harness, cloned into any project, that bootstraps itself, remembers what you have built, and keeps Claude focused.

No Python. No Node. No SQLite. Just files.

---

## 👥 Who is this for

- Solo developers who want structure without ceremony.
- Small teams who need shared context and memory.
- Non-programmers building apps with Claude and tired of repeating themselves.
- Anyone who has ever asked Claude "did we already build this?"

---

## ✨ What you get

- **Two-tier memory** — A searchable ledger of every feature you have built, with automatic archival when it grows.
- **Branch per feature** — Each feature lives on its own branch, keeping `main` clean and the history traceable.
- **Temporary checklists** — Complex features get a `CHECKLIST.md` that fills the memory as tasks are completed, then disappears.
- **Focused subagents** — Code reviewer, security auditor, and QA engineer, invoked only when you ask for them.
- **Modular rules** — Code style, conventions, and testing live in their own files, loaded on demand.
- **Project structure** — A living map of your project, kept up to date.
- **Design system slot** — Drop your design guide in, and Claude respects it.
- **Self-configuring** — First session detects it is unconfigured and starts the setup automatically.
- **Personal overrides** — Keep your own preferences private, never committed.
- **Harness-owned core** — `CLAUDE.md` is infrastructure. It is never edited by the user. Project context lives in `OVERVIEW.md` and `STACK.md`.
- **One-command update** — Update the harness without touching your project files.

---

## 📁 Structure

```
your-project/
├── CLAUDE.md                       # Harness infrastructure (never edit)
├── OVERVIEW.md                     # What the project is (committed)
├── STACK.md                        # Tech stack (committed)
├── DESIGN.md                       # Design system (committed, optional)
├── STRUCTURE.md                    # Project map (committed)
├── harness-verified.json           # Setup state flag
├── harness-manifest.json           # Harness version and file list
├── .gitignore                      # Excludes personal files
├── .claude/
│   ├── settings.json               # Shared permissions (committed)
│   ├── settings.local.json         # Personal permissions (gitignored)
│   ├── custom-instructions.md      # Project-wide custom rules (committed)
│   ├── user-instructions.md        # Your preferences (gitignored)
│   ├── agents/
│   │   ├── code-reviewer.md        # Reviews code for bugs and improvements
│   │   ├── security-auditor.md     # Audits code for vulnerabilities
│   │   └── qa-engineer.md          # Runs types, lint, and tests
│   ├── commands/
│   │   ├── setup-harness.md        # Configure the harness
│   │   ├── update-harness.md       # Update the harness
│   │   ├── document-project.md     # Fill OVERVIEW, STACK, STRUCTURE, DESIGN
│   │   ├── find-feature.md         # Search active memory
│   │   ├── compact-features.md     # Archive old features
│   │   ├── review-code.md          # Run the code reviewer subagent
│   │   ├── audit-security.md       # Run the security auditor subagent
│   │   └── qa-automation.md        # Run the QA engineer subagent
│   └── rules/
│       ├── code-style.md           # Formatting, naming, style rules
│       ├── conventions.md          # Commits, branches, patterns
│       ├── features-format.md      # Format for memory entries
│       ├── git.md                  # Harness Git rules (never edit)
│       ├── custom-git.md           # Your own Git rules (committed)
│       └── testing.md              # Testing framework, structure, commands
└── memory/
    ├── FEATURES.md                 # Active memory (last ~100 features)
    ├── FEATURES-HISTORY.md         # Archived features
    └── CHECKLIST.md                # Temporary, per-feature (gitignored)
```

### What gets committed and what does not

| File | Committed? | Why |
|------|------------|-----|
| `CLAUDE.md` | ✅ Yes | Harness infrastructure |
| `OVERVIEW.md`, `STACK.md` | ✅ Yes | Shared project context |
| `DESIGN.md`, `STRUCTURE.md` | ✅ Yes | Shared project docs |
| `.claude/rules/*` | ✅ Yes | Shared project rules |
| `.claude/custom-instructions.md` | ✅ Yes | Shared project instructions |
| `.claude/user-instructions.md` | ❌ No | Personal preferences |
| `.claude/settings.local.json` | ❌ No | Personal permissions |
| `memory/CHECKLIST.md` | ❌ No | Temporary, per-feature |
| `memory/*` | ✅ Yes | Shared feature memory |

---

## 📦 How to install

### Recommended: ask Claude

The easiest way. Open Claude Code in your project and paste this prompt:

```
Install Minimal Claudeness in this project.
Docs: https://github.com/Mathiew82/minimal-claudeness

If you find conflicts with the project's current configuration
(existing CLAUDE.md, skills, commands, etc.), ask me how to resolve
each one before overwriting anything.

When done, tell me to close and reopen Claude Code to activate the harness.
```

Claude will read the docs, clone the harness, copy the files into your
project, and run the setup. No manual steps.

### Manual install

If you prefer to do it yourself, follow the steps below.

Make sure your project folder already exists before running these commands.
These commands copy the harness files into your project. If you have
existing files with the same names (`CLAUDE.md`, `OVERVIEW.md`, `STACK.md`,
`DESIGN.md`, `STRUCTURE.md`, `harness-verified.json`, `harness-manifest.json`,
or any file inside `.claude/`), resolve the conflict first — decide whether
to keep yours or let the harness version replace it. Minimal Claudeness
comes with its own structure and conventions, and files with reserved
names are managed by the harness.

**Step 1 — Clone the harness:**

```bash
git clone https://github.com/Mathiew82/minimal-claudeness.git
```

**Step 2 — Copy the harness files into your project:**

<details>
<summary>Linux / macOS</summary>

```bash
cd minimal-claudeness
rsync -av --exclude='.git' --exclude='README.md' --exclude='LICENSE' --exclude='.github' --exclude='.gitignore' . ../your-project/
cat .gitignore >> ../your-project/.gitignore
cd ..
```
</details>

<details>
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

**Step 3 — Clean up:**

Once the files are copied, you can safely delete the `minimal-claudeness`
folder — you no longer need it.

<details>
<summary>Linux / macOS</summary>

```bash
rm -rf minimal-claudeness
```
</details>

<details>
<summary>Windows (PowerShell)</summary>

```powershell
Remove-Item -Path "minimal-claudeness" -Recurse -Force
```
</details>

### Activate

If you installed the harness manually while Claude Code was open,
close and reopen Claude Code. The new commands are only loaded at
session start.

Once Claude Code is open again, send any message. The harness will
detect it is not configured and start the setup automatically.

You will see:

> ⌛ Minimal Claudeness is being configured...

Then it will:
- Analyze your project.
- Fill in `OVERVIEW.md` and `STACK.md` (if the project has content).
- Generate `STRUCTURE.md` from your directory tree.
- Fill in `DESIGN.md` (if the project has a UI).
- Create `.claude/user-instructions.md` and `.claude/custom-instructions.md` for you.
- Ensure your `.gitignore` has the three required lines.
- Mark the harness as verified.
- Show you what is available.

No confirmation needed. Just open Claude Code and say hi.

> **Note:** If your project was empty when you installed the harness,
> `OVERVIEW.md`, `STACK.md`, and `DESIGN.md` were left with placeholders.
> Once the project has real content, run `/document-project` to fill them
> in automatically. `STRUCTURE.md` updates itself as you work — you never
> need to touch it.

### Work normally

Before implementing a feature, Claude reads `memory/FEATURES.md` and checks if something similar already exists. If it does, it stops and asks.

For meaningful features, Claude creates a `feat/<short-name>` branch and a temporary `memory/CHECKLIST.md`. As tasks are completed, they are marked in the checklist and summarized into `memory/FEATURES.md`. When the feature is done, the checklist is deleted and the branch is ready for review.

The active memory never exceeds 100 entries. When a new feature would push the count past 100, the oldest entry is automatically moved to `FEATURES-HISTORY.md`.

---

## 🔄 How to update

Run the update command from Claude Code:

```
/update-harness
```

Or, if you prefer to send a prompt:

```
Run /update-harness to update Minimal Claudeness.
Docs: https://github.com/Mathiew82/minimal-claudeness
```

Claude will compare your current version against the latest release,
show you exactly which files will be updated, ask for confirmation, and
then apply the update. Your project files (`OVERVIEW.md`, `STACK.md`,
`DESIGN.md`, `STRUCTURE.md`, `memory/*`, custom rules, personal
instructions) are never touched.

The list of harness-owned files lives in `harness-manifest.json`.

---

## 🗑️ How to uninstall

Ask Claude to remove Minimal Claudeness from the project:

```
Uninstall Minimal Claudeness from this project.
Ask me before deleting anything that was not created by the harness,
and leave my project files untouched.
Docs: https://github.com/Mathiew82/minimal-claudeness
```

Claude will go through the harness files one by one, ask you what to do
when something is ambiguous, and leave anything that belongs to you or
your project intact.

---

## 📟 Commands

| Command | What it does |
|---------|--------------|
| `/setup-harness` | Configures Minimal Claudeness for a new project. |
| `/update-harness` | Updates the harness to the latest version. |
| `/find-feature <term>` | Searches active memory. |
| `/find-feature --all <term>` | Searches active memory and the archive. |
| `/compact-features` | Archives the oldest entries to history. |
| `/review-code` | Runs the code reviewer subagent. |
| `/audit-security` | Runs the security auditor subagent. |
| `/qa-automation` | Runs the QA engineer subagent. |
| `/document-project` | Fills or refreshes OVERVIEW, STACK, STRUCTURE, and DESIGN. |

---

## 🤖 Agents

| Agent | Model | When to use |
|-------|-------|-------------|
| `@code-reviewer` | Sonnet | After code changes, before commit. |
| `@security-auditor` | Sonnet | When auth, payments, or user input is involved. |
| `@qa-engineer` | Haiku | When you want types, lint, and tests checked. |

Each agent is **read-only**. None of them modify your files. They report, you decide.

---

## 🧠 The memory system

Minimal Claudeness uses two files to track what has been built:

**`memory/FEATURES.md`** — Active memory. The most recent ~100 features. Read by Claude before implementing anything new. The file has a counter at the top (`**Count: N / 100**`) that tracks how many entries it contains.

Example entry:

```
## 2024-05-10 - Contact page with form
- **Keywords:** contact, form, smtp, email
- **Files:** src/pages/Contact.tsx, src/api/mail.ts
```

**`memory/FEATURES-HISTORY.md`** — Archive. Older entries, kept forever, read only when you explicitly ask for it (`/find-feature --all`).

The format is defined in `.claude/rules/features-format.md`.

### Feature workflow

1. **Search** — Claude checks `memory/FEATURES.md` for related work.
2. **Branch** — For meaningful features, Claude creates `feat/<short-name>`.
3. **Checklist** — For complex features, Claude creates a temporary `memory/CHECKLIST.md`.
4. **Implement** — Work happens on the branch, checklist updates as tasks complete.
5. **Record** — Meaningful deliverables are appended to `memory/FEATURES.md` with keywords and files.
6. **Close** — When done, `memory/CHECKLIST.md` is deleted. The branch is ready for review.

---

## 🎨 Customization

| File | What to put in it |
|------|-------------------|
| `OVERVIEW.md` | What the project is, who it's for, its purpose. |
| `STACK.md` | Languages, frameworks, versions, key libraries. |
| `DESIGN.md` | Your design system (colors, typography, components). |
| `STRUCTURE.md` | A map of your project structure. |
| `.claude/rules/code-style.md` | Formatting, naming, style rules. |
| `.claude/rules/conventions.md` | Commits, branches, patterns. |
| `.claude/rules/testing.md` | Testing framework, structure, commands. |
| `.claude/rules/features-format.md` | Format for memory entries. |
| `.claude/rules/git.md` | Harness Git rules (do not edit). |
| `.claude/rules/custom-git.md` | Your own Git rules (committed, never overwritten). |
| `.claude/custom-instructions.md` | Project-wide custom instructions (committed). |
| `.claude/user-instructions.md` | Your personal preferences (gitignored). |

The rules files are empty by default with clear placeholders. Fill them when you need them, not before.

### What NOT to edit

- **`CLAUDE.md`** — Harness infrastructure. Managed by Minimal Claudeness and updated when you update the harness. Do not edit it.
- **`.claude/rules/git.md`** — Harness Git rules. Updated with the harness. Do not edit. For your own rules, use `custom-git.md`.
- **`harness-verified.json`** — Managed automatically by the setup.
- **`harness-manifest.json`** — Updated by the update process.

If you want to change project context, edit `OVERVIEW.md` or `STACK.md`.
If you want to add project rules, edit `.claude/rules/` or `.claude/custom-instructions.md`.
If you want personal preferences, edit `.claude/user-instructions.md`.

---

## 🧭 Philosophy

- **Minimal.** If it is not necessary, it is not here.
- **No dependencies.** Pure text, pure Git, pure Claude.
- **Explicit over automatic.** You decide when to invoke agents, not the model.
- **Memory that scales.** Two tiers, archived forever, searchable on demand.
- **Traceable work.** Every feature has a branch, a memory entry, and (if complex) a checklist.
- **Clean separation.** Harness files are updated. Project files are yours.
- **Yours.** Personal instructions stay private, project rules stay shared.

> Claude Code is powerful on its own. Minimal Claudeness just gives it a place to think.

---

## ♻️ How it works

```mermaid
flowchart TD
    A([📱 Open Claude Code]) --> B([✍️ Say hi harness])
    B --> C{🤖 Already configured?}
    
    C -- No --> D([⚙️ Auto-setup<br/>Analyzes project<br/>Fills OVERVIEW, STACK, DESIGN<br/>Generates STRUCTURE])
    C -- Yes --> E([💬 Ask Claude for something])
    D --> E
    
    E --> F{🧭 Feature or small change?}
    
    F -- Small change<br/>styling, typo, button --> G([⚡ Direct<br/>No branch, no checklist<br/>no memory entry])
    
    F -- Feature<br/>form, service, module --> H([🔍 Search memory<br/>for duplicates])
    H --> I([🌿 Create feat/branch])
    I --> J([📝 Implement])
    J --> K([💾 Register in FEATURES.md])
    
    G --> L{❓ Claude asks<br/>commit, push, merge, delete branch?}
    K --> L
    
    L --> M([✅ You decide])

    classDef user fill:#4F46E5,stroke:#312E81,color:#fff,stroke-width:2px
    classDef decision fill:#F59E0B,stroke:#B45309,color:#fff,stroke-width:2px
    classDef system fill:#10B981,stroke:#047857,color:#fff,stroke-width:2px
    classDef quick fill:#6B7280,stroke:#374151,color:#fff,stroke-width:2px
    classDef memory fill:#8B5CF6,stroke:#6D28D9,color:#fff,stroke-width:2px
    classDef action fill:#3B82F6,stroke:#1E40AF,color:#fff,stroke-width:2px
    classDef success fill:#10B981,stroke:#047857,color:#fff,stroke-width:2px

    class A,B,E user
    class C,F,L decision
    class D system
    class G quick
    class H,I memory
    class J,K action
    class M success
```

---

## 🤝 Contributing

Found a bug? Have an idea? Open an issue or a PR.

If you build something cool with Minimal Claudeness, I want to hear about it.

---

<p align="center">
  <strong>Minimal Claudeness</strong><br>
  <em>The essence of working with Claude Code.</em>
</p>
