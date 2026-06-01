# SYSTEM.md — Full Methodology & Blueprint

This document explains the full design of the Second Brain system in detail.
It covers the learning method, Zettelkasten implementation, session structure, and long-term plan.

---

## Part 1 — The Learning Philosophy

### Why Most University Studying Fails

Most students study by:
1. Re-reading slides (passive — barely works)
2. Highlighting notes (feels productive — isn't)
3. Cramming before exams (sticks for days, gone in weeks)

The result: you pass the exam but don't actually know anything three months later.

### What Actually Works (The Science)

| Technique | Effectiveness | Why |
|-----------|--------------|-----|
| **Retrieval practice** | Very high | Recalling info strengthens memory more than re-reading |
| **Spaced repetition** | Very high | Review at increasing intervals before you forget |
| **Elaborative interrogation** | High | Asking "why" and "how" forces deeper processing |
| **Concrete examples** | High | Abstract → concrete = easier to remember and apply |
| **Interleaving** | Medium-High | Mixing topics builds flexible knowledge |
| Re-reading | Low | Familiarity ≠ knowledge |
| Highlighting | Very low | Passive, no recall required |

This system uses the top four.

---

## Part 2 — The Three-Phase Cycle

### Phase 1: Ingestion (Claude teaches you)

**Goal:** Get a clear mental model of the entire module before touching the raw materials.

**How it works:**
1. Drop the raw module folder into the session (ZIPs, PDFs, slides)
2. Claude reads everything
3. Claude teaches you the content — structured, analogies-first, fundamentals before detail
4. You don't read raw slides. Claude does that work.

**Time per module:** 1–2 hours (reading + teaching session)

**Output:** A clear mental map of the module. You should be able to explain the main topics out loud.

---

### Phase 2: Active Recall (You retrieve, Claude fills gaps)

**Goal:** Find out what actually stuck vs what felt like it stuck.

**How it works:**
1. Close all notes
2. Open a blank document
3. Write everything you can remember from Phase 1 — no peeking
4. Bring that back to Claude
5. Claude identifies what's missing, what's wrong, and fills the gaps
6. Repeat on anything that didn't stick after 24 hours

**This is the most important phase.** The discomfort of not remembering is the learning happening.

**Time:** 45–60 minutes, done 24 hours after Phase 1

---

### Phase 3: Testing (Exam-style application)

**Goal:** Move from "I understand this" to "I can use this."

**How it works:**
1. Claude generates scenario-based questions (real-world situations, not "define X")
2. You write full answers as if in an exam
3. Claude gives structured feedback: what was right, what was wrong, what was missing
4. Harder questions on anything that came up weak

**Example question format:**
> "A company stores user passwords using MD5 with no salt. Their database gets breached.
> What is the attack? Why does the current implementation make it worse?
> What should they have done instead?"

**Time:** 1 hour per module

---

## Part 3 — Zettelkasten Implementation in Obsidian

### What is Zettelkasten?

Created by sociologist Niklas Luhmann, who wrote 70+ books using it. The idea:

- Every **concept** gets one atomic note
- Notes link to other notes via `[[WikiLinks]]`
- Over time, a web of connected knowledge forms
- New learning attaches to existing notes — it compounds

It's the opposite of folders-by-subject. Knowledge doesn't care about module boundaries.

### Note Types in This System

| Type | Purpose | Example |
|------|---------|---------|
| **Concept note** | One atomic idea | `Hash Functions.md` |
| **MOC (Map of Content)** | Overview of a topic area | `MOC - Cryptography.md` |
| **Module note** | Index of all concepts in a module | `WM242 ISS.md` |
| **Connection note** | Links two concepts from different modules | `Encryption in Network Protocols.md` |

### Atomic Note Template

```markdown
# [Concept Name]

**Module:** [[WM242 ISS]]
**Topic area:** Cryptography
**Tags:** #module/ISS #topic/[area] #status/[draft|reviewed|mastered]

---

## What is it? (One line)
[Single sentence definition]

## The Analogy
[Simple, relatable analogy that captures the core idea]

## How it works
[Key points — keep it brief, link to sub-concepts rather than explaining inline]

## Why it matters
[What problem does this solve? Where is it used in the real world?]

## Key things to remember
- [ ] [Fact 1]
- [ ] [Fact 2]
- [ ] [Fact 3]

## Connected concepts
- [[Concept A]] — [why it's related]
- [[Concept B]] — [why it's related]

## Questions I can be asked
- [Exam-style question this concept appears in]

---
*Last reviewed: [date]*
```

### Example Completed Note

```markdown
# Hash Functions

**Module:** [[WM242 ISS]]
**Topic area:** Cryptography
**Tags:** #module/ISS #topic/cryptography #status/reviewed

---

## What is it?
A one-way mathematical function that converts any input into a fixed-length fingerprint.

## The Analogy
A meat grinder. You can put any amount of raw meat in, you always get the same
type of minced output, and you can never reconstruct the original steak from it.
Put the same steak in twice → same mince. Put a slightly different steak in → completely
different mince.

## How it works
- Input: any length (a word, a file, an entire database)
- Output: fixed-length string (e.g. SHA-256 always gives 64 hex characters)
- Deterministic: same input → always same output
- Avalanche effect: one bit change in input → completely different output

## Why it matters
Used everywhere: password storage, file integrity checks, digital signatures, blockchain.
You never store a password — you store its hash. On login, hash what user types and compare.

## Key things to remember
- [ ] MD5 = 128-bit, broken — do not use
- [ ] SHA-1 = 160-bit, deprecated — do not use
- [ ] SHA-256 = current standard
- [ ] Argon2 = best for passwords (slow by design, resists brute force)
- [ ] Preimage resistance = can't reverse hash to find input
- [ ] Collision resistance = can't find two inputs with same hash

## Connected concepts
- [[Salting]] — adding random value before hashing to prevent rainbow tables
- [[HMAC]] — hash + secret key = authentication, not just integrity
- [[Digital Signatures]] — uses hash to create a message fingerprint
- [[Rainbow Tables]] — precomputed hash tables used to crack unsalted hashes

## Questions I can be asked
- "A system stores passwords as MD5 hashes with no salt. What attack is possible and how do you fix it?"
- "What is the difference between preimage resistance and collision resistance?"

---
*Last reviewed: June 2026*
```

---

## Part 4 — Long-Term Schedule

### Realistic Timeline for 6 Modules

Assuming **1–2 focused hours per day:**

| Week | Activity |
|------|---------|
| 1–2 | Module 1: ISS (Phase 2 + 3 + Obsidian notes) |
| 3–4 | Module 2: Phase 1 + 2 + 3 + notes |
| 5–6 | Module 3: Phase 1 + 2 + 3 + notes |
| 7–8 | Module 4: Phase 1 + 2 + 3 + notes |
| 9–10 | Module 5: Phase 1 + 2 + 3 + notes |
| 11–12 | Module 6: Phase 1 + 2 + 3 + notes |
| 13+ | Cross-module review, connection notes, spaced repetition |

This is Year 1 content. You'll do the same for Year 2 and Year 3 content as it arrives — but now with a foundation to attach it to.

### Spaced Repetition Schedule

After a note is created:
- Review after 1 day
- Review after 3 days
- Review after 1 week
- Review after 2 weeks
- Review after 1 month

Obsidian's Spaced Repetition plugin can automate this.

---

## Part 5 — GitHub Page Plan

The `README.md` is written to work as a GitHub repository landing page.

**To set up:**
1. Create a new GitHub repo: `second-brain` or `uni-knowledge-system`
2. Push this folder (excluding raw module materials — keep those local)
3. Enable GitHub Pages on the repo
4. The README becomes your public-facing system overview

**What to push:** README.md, SYSTEM.md, CLAUDE.md, Obsidian notes (once created)
**What NOT to push:** Raw module ZIP/PDF files (too large, potentially sensitive)

---

## Part 6 — Session Checklist

Before every learning session:
- [ ] What module/topic am I working on?
- [ ] Which phase am I in?
- [ ] What did I cover last time? (check CLAUDE.md progress log)
- [ ] What is today's goal? (one topic? one full phase?)

After every session:
- [ ] Update the progress log in CLAUDE.md
- [ ] Create or update Obsidian notes for what was covered
- [ ] Schedule next review date

---

## Part 7 — The Compounding Effect

Here's why this system is worth building properly:

- **Year 1:** You learn Module 1. It's hard, starts from zero.
- **Year 1:** You learn Module 2. Some concepts link back to Module 1. Easier.
- **Year 2:** New modules build on Year 1 foundations. Your existing notes give you hooks.
- **Year 3:** You're not learning from scratch — you're adding to a rich web of knowledge.

A student who builds this system in Year 1 will find Year 3 dramatically easier than one who starts fresh each exam season. That's the compound interest of learning done properly.

---

*System designed: June 2026*
*Author: Syed*
*AI assistant: Claude*
