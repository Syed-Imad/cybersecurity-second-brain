# Cybersecurity Second Brain

> A personal knowledge system for building deep, lasting understanding of cybersecurity —
> across 3 years of university, work experience, and self-study.
> Raw materials go in. Claude processes them. Distilled, linked, analogy-rich notes come out.

---

## Table of Contents

1. [How the System Works](#1-how-the-system-works)
2. [Folder Structure](#2-folder-structure)
3. [Adding a New Module — Step by Step](#3-adding-a-new-module--step-by-step)
4. [Claude Prompts — Exact Commands](#4-claude-prompts--exact-commands)
5. [The Three Types of Notes](#5-the-three-types-of-notes)
6. [Setting Up Obsidian](#6-setting-up-obsidian)
7. [Learning Methods](#7-learning-methods)
8. [Querying the Knowledge Base](#8-querying-the-knowledge-base)
9. [Learning Logs — Continuing Across Sessions](#9-learning-logs--continuing-across-sessions)
10. [GitHub](#10-github)
11. [Progress Tracker](#11-progress-tracker)
12. [Dos and Don'ts](#12-dos-and-donts)
13. [Quick Reference Card](#13-quick-reference-card)

---

## 1. How the System Works

```
┌──────────────────────────────────────────────────────────────────┐
│                                                                    │
│  YOU                                                               │
│  Drop raw files (slides, PDFs, ZIPs) into Raw Materials/          │
│                         │                                          │
│                         ▼                                          │
│  CLAUDE CODE                                                       │
│  Reads everything. Generates three things:                        │
│  · Atomic Zettelkasten notes (for linking + querying)             │
│  · A readable Study Guide (for actually learning from)            │
│  · A Learning Log (so you can continue another day)               │
│                         │                                          │
│                         ▼                                          │
│  KNOWLEDGE BASE                                                    │
│  Clean markdown you can study, navigate in Obsidian,              │
│  query with Claude, and feed to other AI models.                  │
│                                                                    │
└──────────────────────────────────────────────────────────────────┘
```

**You never read raw slides.** Claude does that work. What you get is the distilled essence of every concept — explained with an analogy, structured clearly, linked to related ideas across every module.

**Why Zettelkasten?** Instead of notes siloed by module, every concept is its own atomic file. A note on `Hash Functions` links to `Salting`, `HMAC`, `Digital Signatures`, and `Preimage Resistance` regardless of which year or module they came from. New modules don't create new silos — they enrich the existing web. By Year 3 you have a dense connected knowledge graph, not 6 separate piles of notes.

---

## 2. Folder Structure

```
cybersecurity-second-brain/
│
├── 📁 Raw Materials/                 ← YOUR INPUT — drop files here
│   ├── Year 1/ (Modules 1–6)
│   ├── Year 2/ (Modules 1–6)        ← WM242 ISS lives here
│   ├── Year 3/ (Modules 1–6 + Dissertation)
│   ├── Work & Internships/
│   └── Courses/ (TryHackMe, Other)
│
├── 📁 Knowledge Base/                ← CLAUDE'S OUTPUT — open this in Obsidian
│   │
│   ├── Concepts/                     ← atomic Zettelkasten notes (one per concept)
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
│   │
│   ├── Study Guides/                 ← readable narrative explanations per module
│   │   └── WM242 ISS — Study Guide.md  ✅
│   │
│   ├── MOC/                          ← Maps of Content (navigation hubs per module)
│   └── Index/                        ← master index across everything
│
├── 📁 Learning Logs/                 ← session records — continue learning any day
│   ├── README.md                     ← index of all sessions + querying guide
│   └── 2026-06-01 — WM242 — Phase 1 — Full Ingestion.md  ✅
│
├── 📁 Templates/                     ← Claude uses these when generating notes
│   ├── Concept-Note.md
│   ├── Module-Overview.md
│   ├── Work-Role.md
│   └── Learning-Log.md
│
├── CLAUDE.md                         ← Claude reads this at the start of every session
├── SYSTEM.md                         ← full methodology and blueprint
└── README.md                         ← this file
```

### What each folder is for

| Folder | Purpose | You interact by |
|--------|---------|----------------|
| `Raw Materials/` | Source files — slides, ZIPs, PDFs | Dropping files in |
| `Knowledge Base/Concepts/` | Atomic notes — for linking, querying, Obsidian graph | Reading individual concepts |
| `Knowledge Base/Study Guides/` | Readable narrative — for actually studying | Reading top to bottom |
| `Knowledge Base/MOC/` | Navigation hubs — one per module | Jumping to topic areas |
| `Learning Logs/` | Session history — for continuity across days | Pointing Claude at the latest log |

> **Raw Materials are NOT pushed to GitHub.** PDFs, ZIPs, and videos are excluded by `.gitignore`. Only the Knowledge Base and Learning Logs (clean markdown) go to GitHub.

---

## 3. Adding a New Module — Step by Step

### Step 1 — Get your files
Download module materials from your university portal. Usually weekly ZIP files or individual PDFs per week.

### Step 2 — Drop files into Raw Materials
```
Raw Materials/Year X/Module Y - [Module Name]/
```
Dump everything in. Don't organise — Claude handles that.

> WM242 ISS is a special case — materials already exist at:
> `/Users/syedimaduddin/Documents/ISS Module Materials (ALL)`
> No need to move them. Just point Claude at that path.

### Step 3 — Open Claude Code in this project
```bash
cd "/Users/syedimaduddin/Documents/Claude/Cybersecurity Second Brain"
claude
```

### Step 4 — Run the ingestion prompt
```
Read CLAUDE.md and my latest log in Learning Logs/.
Then ingest Raw Materials/Year 2/Module 2 - [name]/
Generate:
1. Atomic concept notes in Knowledge Base/Concepts/
2. A readable Study Guide in Knowledge Base/Study Guides/
3. A MOC in Knowledge Base/MOC/
4. A learning log in Learning Logs/
```

### Step 5 — Review, then push
```bash
git add -A
git commit -m "Add [Module Name] — Phase 1 complete, 20 notes generated"
git push
```

---

## 4. Claude Prompts — Exact Commands

### Starting any session
```
Read CLAUDE.md and my latest log in Learning Logs/
Then [tell me what we're doing today]
```

### Ingesting a module
```
Read CLAUDE.md and ingest Raw Materials/Year 2/Module 2 - [name]/
Generate atomic concept notes, a study guide, a MOC, and a learning log.
```

### Being taught a topic
```
Read CLAUDE.md and teach me [topic] using an analogy and examples.
Start with the problem it solves before explaining how it works.
```

### Active recall (Phase 2)
```
I'm doing active recall on [module]. I'll write what I remember — don't help yet.
After I paste, tell me: what I got wrong, what I missed, and what to focus on next.
```

### Getting quizzed (Phase 3)
```
Quiz me on [topic] with scenario-based questions.
One at a time. Wait for my full answer before the next question.
Give detailed feedback after each answer.
```

### Continuing from a previous session
```
Read CLAUDE.md and Learning Logs/[date — module — phase].md
Pick up where we left off.
```

### Finding cross-module connections
```
Read all notes in Knowledge Base/Concepts/ and find concepts that appear
in multiple modules but aren't yet linked. Add [[WikiLinks]] between them.
```

### Querying your knowledge base
```
Read Knowledge Base/Concepts/[folder]/ and explain how [concept A]
and [concept B] relate to each other.
```

### Feeding notes to another AI
```
Read all notes in Knowledge Base/Concepts/[folder]/ and produce a single
clean summary block I can paste into another AI model as context.
```

### Ending a session
```
Write a learning log for this session and save it to
Learning Logs/[YYYY-MM-DD] — [Module] — [Phase] — [Topic].md
Use the template in Templates/Learning-Log.md
```

---

## 5. The Three Types of Notes

The Knowledge Base has three distinct note types. Each one serves a different purpose.

### Concept Notes (Concepts/)
Atomic, single-concept files in Zettelkasten format. The backbone of the system.

```markdown
# Hash Functions

## What is it?
One sentence definition.

## The Analogy
A meat grinder. One-way, deterministic, irreversible.

## Key points
- Tables, bullets, facts
- Links to related concepts

## Connected concepts
- [[Salting]]
- [[HMAC]]
- [[Digital Signatures]]
```

**Use for:** Quick lookup, following concept chains, Obsidian graph, querying with Claude, feeding to AI models.
**Not for:** Reading a whole topic from start to finish.

---

### Study Guides (Study Guides/)
Narrative, flowing documents covering an entire module. Designed to be read.

> Written in full sentences and paragraphs, not bullets.
> Every concept explained with its analogy, context, and connections.
> Like a well-written textbook chapter — but generated from your actual module content.

**Use for:** First pass learning, revision before exams, sharing with others.
**Not for:** Quick lookup or querying — too long for that.

---

### MOCs — Maps of Content (MOC/)
Navigation hubs. One per module. Lists every concept note for that module with links.

**Use for:** Getting an overview, jumping to specific concept areas, tracking Phase 2 and 3 progress checklists.

---

## 6. Setting Up Obsidian

### Which folder to open as your vault
**Open `Knowledge Base/` only** — not the whole project folder.

```
Obsidian → Open folder as vault →
/Users/syedimaduddin/Documents/Claude/Cybersecurity Second Brain/Knowledge Base/
```

Why not the whole folder? Raw Materials, logs, and system files would clutter the graph and search. Knowledge Base is clean notes only.

### Recommended plugins

| Plugin | What it does |
|--------|-------------|
| **Dataview** | Query notes like a database — filter by tag, module, status |
| **Templater** | Auto-fill note templates when creating new notes |
| **Spaced Repetition** | Built-in flashcard review at increasing intervals |
| **Calendar** | Visual tracker of which days you studied |
| **Graph View** | Built-in — see your entire knowledge web as a visual graph |

### Key views in Obsidian

**Graph View (Cmd+G):** Every note is a node. Every `[[link]]` is a connection. As you add modules, the graph grows denser. Topics with many connections are your core knowledge. Isolated nodes need more linking.

**Search (Cmd+F):** Full-text search across all notes instantly. Search `#topic/hashing` to see all hashing notes. Search `AES` to see every note that mentions AES.

**Dataview — paste these into any note:**

See all notes for a module:
````
```dataview
TABLE tags
FROM "Concepts"
WHERE contains(tags, "WM242")
SORT file.name ASC
```
````

See everything not yet reviewed:
````
```dataview
LIST
FROM "Concepts"
WHERE !contains(tags, "reviewed")
```
````

---

## 7. Learning Methods

Four methods in order of effectiveness. Don't skip straight to passive reading.

### Method 1 — Read the Study Guide (passive — first pass only)
Open `Knowledge Base/Study Guides/[Module] — Study Guide.md` and read through once. This gives you the mental map before anything else. Don't rely on this alone — retention from reading alone is poor.

### Method 2 — Active Recall (strongest — do this always)
The most evidence-backed learning method. Forces retrieval rather than recognition.

**How:**
1. Close everything
2. Open a blank document
3. Write everything you remember about the topic — no peeking
4. Bring it back to Claude

**Prompt:**
```
Here's my active recall on [topic]: [paste]
Tell me exactly: what I got wrong, what I missed, what was vague.
Be specific — not "you missed hashing" but "you didn't mention preimage resistance".
```

The discomfort of not remembering is the learning happening. That's the point.

Do this **24 hours after** the Study Guide pass — not immediately.

### Method 3 — Feynman Technique (find fake understanding)
Explain it out loud as if teaching someone who knows nothing. Wherever your explanation breaks down is where your understanding breaks down.

**Prompt:**
```
I'm going to explain [concept] as if teaching it to a complete beginner.
Tell me where my explanation is wrong, vague, or where I'm faking understanding.
[your explanation]
```

### Method 4 — Scenario Testing (application under pressure)
Exam-style questions in realistic scenarios. Moves you from "I understand this" to "I can use this".

**Prompt:**
```
Give me a scenario-based question on [topic].
One at a time. Wait for my full answer before giving feedback.
```

Example question:
> *A company stores passwords as unsalted MD5 hashes. Their database is breached.
> What attack is now possible? Why does the lack of salt make it significantly worse?
> What should they have done instead?*

### Method 5 — Spaced Repetition (long-term retention)
Use Obsidian's Spaced Repetition plugin to review notes at: 1 day → 3 days → 1 week → 2 weeks → 1 month.

This keeps knowledge in long-term memory with minimal time investment per session.

---

## 8. Querying the Knowledge Base

Querying is getting information back out. Two tools: Obsidian for navigation, Claude for synthesis.

### Obsidian (navigation and lookup)
- **Cmd+F** — find any concept instantly
- **Cmd+G** — graph view — see connections visually
- **Dataview** — filter and list notes by any tag or property
- **Backlinks panel** — see every note that links to the current one

### Claude (synthesis and reasoning)

**Compare two concepts:**
```
Read Knowledge Base/Concepts/ and compare RSA and ECC.
When would you choose one over the other, and why?
```

**Find connections you haven't spotted:**
```
Read all notes in Knowledge Base/Concepts/ and tell me which concepts
from different topic folders are closely related but not yet linked.
```

**Topic summary for another AI:**
```
Read Knowledge Base/Concepts/Hashing/ and produce a single clean block
I can paste into another AI as context — no fluff, just the key facts.
```

**Identify weak areas in your notes:**
```
Read all notes in Knowledge Base/Concepts/[folder]/ and tell me which ones
are thinnest — least detail, missing analogies, or fewest links.
```

**Cross-module synthesis (Year 3+ power feature):**
```
Read all notes in Knowledge Base/Concepts/ and explain how the concept of
"trust" appears differently in PKI, SSO, blockchain, and network security.
```

No search engine or textbook can do that last one. That's the second brain working as intended.

---

## 9. Learning Logs — Continuing Across Sessions

Learning Logs solve the continuity problem. Claude has no memory between sessions. Logs give it that memory.

### Every session starts with:
```
Read CLAUDE.md and my latest log in Learning Logs/
[then tell Claude what you want to do today]
```

Claude reads where you left off, what you struggled with, and the exact pickup instruction from the previous session.

### Every session ends with:
```
Write a learning log for this session using Templates/Learning-Log.md
Save it to Learning Logs/[YYYY-MM-DD] — [Module] — [Phase] — [Topic].md
```

### What a log captures:
- What was covered
- What analogies and approaches worked well (so they're reused)
- What didn't click and needs revisiting
- Gaps and weak areas to probe next time
- Exact instruction for where to pick up

### Querying across all logs:
```
Read all files in Learning Logs/ and tell me:
- Which topics have I covered?
- Which ones have I consistently struggled with?
- What's incomplete or hasn't had Phase 2/3 yet?
- Where should I start today?
```

---

## 10. GitHub

### First-time push
1. Create repo at [github.com/new](https://github.com/new) — name: `cybersecurity-second-brain`, Public
2. Run:
```bash
cd "/Users/syedimaduddin/Documents/Claude/Cybersecurity Second Brain"
git remote add origin https://github.com/YOUR-USERNAME/cybersecurity-second-brain.git
git push -u origin main
```

### Regular updates (after any session)
```bash
git add -A
git commit -m "Add [description]"
git push
```

### What's on GitHub vs what stays local

| Pushed to GitHub | Stays local only |
|-----------------|-----------------|
| All Knowledge Base notes | Raw PDFs |
| Study Guides | ZIP files |
| Learning Logs | MP4 lecture videos |
| README, CLAUDE.md, SYSTEM.md | Database files |
| Templates + folder structure | |

### GitHub Pages (optional)
Settings → Pages → Source: main → Save
Creates a live website at: `https://YOUR-USERNAME.github.io/cybersecurity-second-brain`

---

## 11. Progress Tracker

| Module | Raw Materials | Phase 1 | Phase 2 | Phase 3 | Notes |
|--------|:---:|:---:|:---:|:---:|:---:|
| **Y2 — WM242 ISS** | ✅ | ✅ | ⬜ | ⬜ | 20 concept notes, 1 study guide |
| Y1 — Modules 1–6 | ⬜ | ⬜ | ⬜ | ⬜ | Awaiting materials |
| Y2 — Modules 2–6 | ⬜ | ⬜ | ⬜ | ⬜ | Awaiting materials |
| Y3 — Modules 1–6 | ⬜ | ⬜ | ⬜ | ⬜ | Awaiting materials |
| Y3 — Dissertation | ⬜ | — | — | — | Awaiting topic |
| TryHackMe | ⬜ | ⬜ | ⬜ | ⬜ | Ongoing |
| Work & Internships | ⬜ | ⬜ | ⬜ | ⬜ | Ongoing |

---

## 12. Dos and Don'ts

### ✅ Do
- **Always start with:** `Read CLAUDE.md and my latest Learning Log`
- **Open only `Knowledge Base/` in Obsidian** — not the whole project
- **Do Phase 2 at least 24 hours after Phase 1** — sleep on it, the gap matters
- **End every session with a log** — even a short one. Future you will thank you
- **Tell Claude when an analogy doesn't land** — it will find a better one
- **Push to GitHub after every session** — version control protects your work
- **Add TryHackMe writeups to Raw Materials** — practical knowledge belongs in the system too

### ❌ Don't
- **Don't skip active recall** — reading is not learning
- **Don't open the whole project folder in Obsidian** — noise from system files clutters everything
- **Don't start a session without reading your latest log** — you'll repeat yourself and lose continuity
- **Don't copy raw slides into Knowledge Base** — processed notes only
- **Don't push PDFs or videos to GitHub** — `.gitignore` blocks them but be aware
- **Don't try to do everything at once** — one module, all three phases, before moving to the next

---

## 13. Quick Reference Card

| Task | Where | Prompt / Action |
|------|-------|----------------|
| Start any session | Claude Code | `Read CLAUDE.md and my latest log in Learning Logs/` |
| Add new module files | `Raw Materials/Year X/Module Y/` | Drag and drop |
| Ingest a module | Claude Code | `Read CLAUDE.md and ingest Raw Materials/Year 2/Module 2 - [name]/` |
| Read and learn | `Knowledge Base/Study Guides/` in Obsidian | Open the study guide, read top to bottom |
| Look up a concept | `Knowledge Base/Concepts/` in Obsidian | Cmd+F search |
| See knowledge graph | Obsidian | Cmd+G |
| Active recall | Claude Code | `Here's my recall: [paste]. What did I miss?` |
| Get quizzed | Claude Code | `Quiz me on [topic] one question at a time` |
| End session + log | Claude Code | `Write a learning log for this session` |
| Query across all notes | Claude Code | `Read Knowledge Base/Concepts/ and [question]` |
| Feed notes to AI | Claude Code | `Summarise Knowledge Base/Concepts/[folder]/ into one clean block` |
| Push updates | Terminal | `git add -A && git commit -m "..." && git push` |

---

*Started: June 2026 | Syed Imad Uddin*
*Stack: Obsidian · Zettelkasten · Claude Code · GitHub*
