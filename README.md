# Cybersecurity Second Brain

> A personal knowledge system for building deep, lasting understanding of cybersecurity — across 3 years of university, work, and self-study.
> Raw materials go in. Claude processes them. Distilled, linked, analogy-rich notes come out.

---

## Table of Contents

1. [How the System Works](#how-the-system-works)
2. [Folder Structure Explained](#folder-structure-explained)
3. [Step-by-Step: Adding a New Module](#step-by-step-adding-a-new-module)
4. [Claude Prompts — Exact Commands to Use](#claude-prompts--exact-commands-to-use)
5. [Setting Up Obsidian](#setting-up-obsidian)
6. [How the Notes Are Structured](#how-the-notes-are-structured)
7. [The Learning Phases](#the-learning-phases)
8. [GitHub — Pushing Updates](#github--pushing-updates)
9. [Progress Tracker](#progress-tracker)
10. [Dos and Don'ts](#dos-and-donts)

---

## How the System Works

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                   │
│   YOU                                                             │
│   Drop raw lecture slides, PDFs, and ZIPs into Raw Materials/    │
│                        │                                          │
│                        ▼                                          │
│   CLAUDE CODE                                                     │
│   Reads everything. Distils it into atomic, linked,              │
│   analogy-rich Zettelkasten notes.                               │
│                        │                                          │
│                        ▼                                          │
│   KNOWLEDGE BASE                                                  │
│   Clean markdown notes you can learn from, search,              │
│   navigate in Obsidian, and feed to AI models.                   │
│                                                                   │
└─────────────────────────────────────────────────────────────────┘
```

**The core idea:** You never sit and read 300 slides. Claude does that. What you get back is the distilled essence — every concept explained with an analogy, key facts, and links to related ideas. Then you learn from those notes, get tested on them, and over time they compound into a connected web of knowledge.

**Why Zettelkasten?** Instead of notes siloed by module, every concept is its own atomic file. A note on `Hash Functions` links to `Salting`, `HMAC`, `Digital Signatures`, and `Preimage Resistance` — regardless of which module or year they came from. By Year 3 you have a web of interconnected knowledge, not 6 separate piles of notes you've forgotten.

---

## Folder Structure Explained

```
cybersecurity-second-brain/
│
├── 📁 Raw Materials/                ← YOUR INPUT — drop files here
│   ├── Year 1/
│   │   ├── Module 1/                ← empty, ready for your files
│   │   ├── Module 2/
│   │   ├── Module 3/
│   │   ├── Module 4/
│   │   ├── Module 5/
│   │   └── Module 6/
│   ├── Year 2/
│   │   ├── Module 1 - WM242 ISS/    ← has a pointer to your ISS files
│   │   ├── Module 2/
│   │   └── ... (Modules 3–6)
│   ├── Year 3/
│   │   ├── Module 1–6/
│   │   └── Dissertation/
│   ├── Work & Internships/          ← internship docs, notes, resources
│   └── Courses/
│       ├── TryHackMe/               ← room writeups, notes, paths
│       └── Other/                   ← any other courses/certs
│
├── 📁 Knowledge Base/               ← CLAUDE'S OUTPUT — your second brain
│   ├── Concepts/                    ← all atomic notes live here
│   │   ├── Cryptography Foundations/
│   │   ├── Symmetric Cryptography/
│   │   ├── Asymmetric Cryptography/
│   │   ├── Hashing/
│   │   ├── Key Management/
│   │   ├── Digital Signatures and PKI/
│   │   ├── Security Protocols/
│   │   ├── Authentication/
│   │   ├── Cryptanalysis/
│   │   ├── Advanced Cryptography/
│   │   └── Secure System Design/
│   ├── MOC/                         ← Maps of Content — topic navigation hubs
│   └── Index/                       ← master index across all notes
│
├── 📁 Templates/                    ← note templates for Claude to use
│   ├── Concept-Note.md
│   ├── Module-Overview.md
│   └── Work-Role.md
│
├── CLAUDE.md                        ← instructions Claude reads at session start
├── SYSTEM.md                        ← full methodology and blueprint
└── README.md                        ← this file
```

### The Two Folders That Matter Most

| Folder | What it is | You interact with it by |
|--------|-----------|------------------------|
| `Raw Materials/` | Where source files live | Dropping your lecture ZIPs/PDFs in |
| `Knowledge Base/` | Your actual second brain | Opening in Obsidian, reading, studying |

> **Raw Materials are NOT pushed to GitHub.** The `.gitignore` excludes PDFs, ZIPs, and MP4s — they're too large and potentially sensitive. Only the Knowledge Base notes (clean markdown) are tracked and pushed.

---

## Step-by-Step: Adding a New Module

Here is the exact process every single time you get new module content:

### Step 1 — Get your files
Download the module materials from your university portal. You'll usually get:
- A folder of weekly ZIP files (each containing lecture slides + lab PDFs)
- Or individual PDFs per week

### Step 2 — Drop files into Raw Materials
Navigate to the correct year and module folder:
```
Raw Materials/Year X/Module Y - [Module Name]/
```
Dump everything in there. ZIPs, PDFs, whatever you have. Don't organise them — Claude will sort through it.

> **WM242 ISS is a special case.** The files already exist at:
> `/Users/syedimaduddin/Documents/ISS Module Materials (ALL)`
> They don't need to be moved — just point Claude at that path.

### Step 3 — Open Claude Code in this project folder
Open your terminal and run:
```bash
cd "/Users/syedimaduddin/Documents/Claude/Cybersecurity Second Brain"
claude
```
Or open the folder in Claude Code directly from the UI.

### Step 4 — Use the ingestion prompt
Say this to Claude:
```
Read CLAUDE.md, then ingest the module at Raw Materials/Year 2/Module 2 - [name]/
```
Claude will:
1. Read `CLAUDE.md` to understand your learning style
2. Read all the raw files
3. Generate atomic Zettelkasten notes in `Knowledge Base/Concepts/`
4. Create a MOC (Map of Content) in `Knowledge Base/MOC/`
5. Update the progress tracker

### Step 5 — Review what was generated
Open Obsidian (see setup below) and look through the new notes. If anything is unclear, ask Claude to re-explain it with a better analogy.

### Step 6 — Push to GitHub
```bash
git add -A
git commit -m "Add [Module Name] notes — Phase 1 complete"
git push
```

---

## Claude Prompts — Exact Commands to Use

Copy and paste these. They are designed to work with `CLAUDE.md`.

### Starting a session
```
Read CLAUDE.md, then let's work on [Module Name]
```

### Ingesting a new module
```
Read CLAUDE.md, then ingest everything at Raw Materials/Year 2/Module 2 - [name]/ and generate Zettelkasten notes in Knowledge Base/Concepts/
```

### Ingesting WM242 ISS specifically
```
Read CLAUDE.md, then ingest the ISS materials at /Users/syedimaduddin/Documents/ISS Module Materials (ALL) and generate Zettelkasten notes
```

### Getting taught a specific topic
```
Read CLAUDE.md, then teach me [topic] — use an analogy and examples
```

### Active recall (Phase 2)
```
I'm going to do active recall on [module]. Ask me to explain each concept and tell me what I get wrong or miss
```

### Getting quizzed (Phase 3)
```
Quiz me on [module/topic] with exam-style scenario questions. Wait for my answer before giving feedback
```

### Generating a note for a specific concept
```
Create a Zettelkasten note for [concept] using the template in Templates/Concept-Note.md and save it to Knowledge Base/Concepts/[topic folder]/
```

### Checking what's been covered
```
Read CLAUDE.md and tell me what modules have been ingested and what still needs doing
```

### Cross-module connections
```
Look through Knowledge Base/Concepts/ and find any notes from other modules that connect to [topic]. Add [[links]] between them
```

### Feeding notes to another AI
```
Read all notes in Knowledge Base/Concepts/[folder]/ and give me a single clean summary I can paste into another AI
```

---

## Setting Up Obsidian

### Which folder to open as your vault
Open **`Knowledge Base/`** as your Obsidian vault — not the whole project folder.

```
Obsidian → Open folder as vault → select:
/Users/syedimaduddin/Documents/Claude/Cybersecurity Second Brain/Knowledge Base/
```

> **Why just Knowledge Base?** Because Obsidian is for reading and navigating your notes — not your raw slides or system files. Keeping it clean means a better graph view and faster search.

### First time setup in Obsidian
1. Open Obsidian
2. Click **Open folder as vault**
3. Navigate to `Cybersecurity Second Brain/Knowledge Base/`
4. Click Open

### Recommended plugins to install
Go to **Settings → Community Plugins → Browse** and install:

| Plugin | What it does | Why you need it |
|--------|-------------|-----------------|
| **Dataview** | Query your notes like a database | See all notes by status, module, topic |
| **Templater** | Auto-fill note templates | Consistent note structure every time |
| **Spaced Repetition** | Built-in flashcard review | Review notes before you forget them |
| **Calendar** | Track daily study sessions | See which days you studied |
| **Graph View** | Built-in — shows note connections | See your knowledge web visually |

### Useful Obsidian views

**Graph view** (Ctrl/Cmd + G): Shows all your notes as nodes with lines connecting linked concepts. The more you study, the denser and more connected the graph becomes. This is what a second brain looks like visually.

**Dataview query** — paste this into any note to see all reviewed notes:
````
```dataview
TABLE file.mtime as "Last reviewed"
FROM "Concepts"
WHERE contains(tags, "reviewed")
SORT file.mtime DESC
```
````

**Search** (Ctrl/Cmd + F): Search across every note instantly. Type "AES" and every note that mentions AES appears.

---

## How the Notes Are Structured

Every note Claude generates follows the same format:

```markdown
# [Concept Name]

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/hashing #status/reviewed

---

## What is it?
One sentence. No jargon.

## The Analogy
A simple, relatable comparison from everyday life.

## [Main content]
Tables, bullet points, key facts — never walls of text.

## Connected concepts
- [[Related Note 1]] — why it's related
- [[Related Note 2]] — why it's related

---
*Source: WM242 Week X | Last reviewed: [date]*
```

**The `[[double bracket]]` links** are Obsidian WikiLinks. Click any of them in Obsidian and it takes you directly to that note. This is what creates the web.

**The tags** let you filter and query:
- `#module/WM242` — filter by module
- `#year/2` — filter by year
- `#topic/hashing` — filter by topic
- `#status/reviewed` — filter by what you've studied

---

## The Learning Phases

Every module goes through three phases. Don't skip them — each one does something different in your brain.

### Phase 1 — Ingestion (Claude teaches you)
**What:** Claude reads all raw materials and generates Zettelkasten notes.
**You do:** Read through the notes Claude created. Ask for clarification on anything unclear.
**Output:** A mental map of the module. 20–40 atomic notes in Knowledge Base.
**Time:** 1–2 hours per module.

### Phase 2 — Active Recall (you retrieve, Claude corrects)
**What:** You close all notes and write everything you can remember from scratch.
**You do:** Open a blank document. Write every concept you remember — no peeking. Bring it back to Claude. Claude tells you what you missed and what was wrong.
**Why it matters:** The act of retrieving information strengthens memory far more than re-reading. The discomfort of not remembering IS the learning happening.
**Time:** 45–60 minutes, done 24 hours after Phase 1.

Prompt to use:
```
I've done active recall on WM242. Here's what I wrote: [paste your notes]
Tell me what I got wrong, what I missed, and what needs more detail
```

### Phase 3 — Testing (scenario questions)
**What:** Claude generates exam-style questions. You write full answers. Claude gives feedback.
**You do:** Treat it like a real exam. Write complete answers, not bullet points.
**Why it matters:** Moves you from "I understand this" to "I can apply this under pressure."
**Time:** 1 hour per module.

Prompt to use:
```
Quiz me on WM242 with 3 scenario-based questions. One at a time. Wait for my answer before the next question.
```

### Spaced Repetition — ongoing
After Phase 3, use Obsidian's Spaced Repetition plugin to review notes at:
- 1 day after creation
- 3 days later
- 1 week later
- 2 weeks later
- 1 month later

This keeps knowledge in long-term memory with minimal time investment.

---

## GitHub — Pushing Updates

The repo is already initialised with git. After any session where Claude adds new notes:

```bash
cd "/Users/syedimaduddin/Documents/Claude/Cybersecurity Second Brain"
git add -A
git commit -m "Add [description of what was added]"
git push
```

### First-time push (if not done yet)
1. Go to [github.com/new](https://github.com/new)
2. Name it `cybersecurity-second-brain`
3. Set to **Public**, tick nothing else
4. Click Create repository
5. Run:
```bash
cd "/Users/syedimaduddin/Documents/Claude/Cybersecurity Second Brain"
git remote add origin https://github.com/YOUR-USERNAME/cybersecurity-second-brain.git
git push -u origin main
```

### What gets pushed / what doesn't

| Included in GitHub | Excluded (stays local only) |
|-------------------|----------------------------|
| All Knowledge Base notes (.md) | Raw PDFs |
| README, CLAUDE.md, SYSTEM.md | ZIP files |
| Templates | MP4 lecture videos |
| Folder structure | Database files |

This means GitHub shows your clean knowledge base — a public portfolio of what you know — without exposing your university's lecture materials.

### GitHub Pages (optional)
Turn your README into a live webpage:
Settings → Pages → Source: main branch → Save
Your repo becomes a website at: `https://YOUR-USERNAME.github.io/cybersecurity-second-brain`

---

## Progress Tracker

| Module | Raw Materials | Phase 1 | Phase 2 | Phase 3 | Notes in KB |
|--------|:---:|:---:|:---:|:---:|:---:|
| **Y2 — WM242 Implementing Secure Systems** | ✅ | ✅ | ⬜ | ⬜ | 20 |
| Y1 — Module 1 | ⬜ | ⬜ | ⬜ | ⬜ | 0 |
| Y1 — Module 2 | ⬜ | ⬜ | ⬜ | ⬜ | 0 |
| Y1 — Module 3 | ⬜ | ⬜ | ⬜ | ⬜ | 0 |
| Y1 — Module 4 | ⬜ | ⬜ | ⬜ | ⬜ | 0 |
| Y1 — Module 5 | ⬜ | ⬜ | ⬜ | ⬜ | 0 |
| Y1 — Module 6 | ⬜ | ⬜ | ⬜ | ⬜ | 0 |
| Y2 — Modules 2–6 | ⬜ | ⬜ | ⬜ | ⬜ | 0 |
| Y3 — Modules 1–6 | ⬜ | ⬜ | ⬜ | ⬜ | 0 |
| Y3 — Dissertation | ⬜ | — | — | — | 0 |
| TryHackMe | ⬜ | ⬜ | ⬜ | ⬜ | 0 |
| Work & Internships | ⬜ | ⬜ | ⬜ | ⬜ | 0 |

---

## Dos and Don'ts

### ✅ Do
- **Drop raw files and let Claude handle them.** Don't try to summarise slides yourself first.
- **Open only `Knowledge Base/` in Obsidian** — not the whole project.
- **Do Phase 2 at least 24 hours after Phase 1.** Sleep on it. The gap is the point.
- **Push to GitHub regularly.** It's version control — you can always roll back if something gets messy.
- **Tell Claude when an analogy doesn't click.** It will find a different one. This is the whole point of CLAUDE.md.
- **Add TryHackMe writeups to Raw Materials/Courses/TryHackMe/** and ask Claude to turn them into notes — practical knowledge belongs in the Knowledge Base too.

### ❌ Don't
- **Don't copy lecture slides into Knowledge Base.** Raw content is not the second brain — processed notes are.
- **Don't skip the analogy step.** If a note doesn't have an analogy, ask Claude to add one.
- **Don't push raw PDFs or videos to GitHub.** The `.gitignore` blocks them but be aware.
- **Don't try to do everything at once.** One module at a time, all three phases, before moving on.
- **Don't open the whole project folder in Obsidian.** You'll get noise from README files and system docs mixed in with your notes.
- **Don't invent your own note format.** Use the template in `Templates/Concept-Note.md` — consistency is what makes Obsidian's graph and search powerful.

---

## Quick Reference Card

| Task | Where | Prompt / Action |
|------|-------|----------------|
| Add new module files | `Raw Materials/Year X/Module Y/` | Drag and drop |
| Ingest a module | Claude Code in this folder | `"Read CLAUDE.md, ingest Raw Materials/Year X/Module Y/"` |
| Study notes | `Knowledge Base/` in Obsidian | Open vault, browse or search |
| Active recall | Blank document → Claude | `"Here's my recall: [paste]. What did I miss?"` |
| Get quizzed | Claude Code | `"Quiz me on [topic] one question at a time"` |
| Add a specific note | Claude Code | `"Create a Zettelkasten note for [concept]"` |
| Push updates | Terminal | `git add -A && git commit -m "..." && git push` |
| See all notes linked | Obsidian | Cmd+G (Graph view) |
| Find a concept fast | Obsidian | Cmd+F (search) |
| Feed notes to another AI | Claude Code | `"Summarise all notes in Knowledge Base/Concepts/[folder]/ into one block"` |

---

*Started: June 2026 | Syed Imad Uddin*
*AI assistant: Claude Code*
*Stack: Obsidian · Zettelkasten · GitHub*
