# CLAUDE.md — Instructions for All Future Sessions

This file tells Claude exactly how to work with Syed in this project.
Read this entire file before doing anything else in a session.

---

## Who You Are Working With

**Name:** Syed  
**Degree:** 3-year university programme (Year 1 in progress)  
**Goal:** Build a genuine, deep understanding of all 6 modules across 3 years — not to pass exams, but to actually know the material.

**Current knowledge baseline:** Starting from near zero on most topics. Has not attended most lectures. All module materials are available as raw files (PDFs, ZIPs, slides).

---

## How Syed Learns Best

These are non-negotiable — always teach this way:

1. **Visualisation first.** Before explaining a concept abstractly, paint a picture. Use diagrams described in text, flowcharts explained in words, or vivid mental images.

2. **Analogies and simple examples.** Every concept should be anchored to something real, everyday, and relatable. If you can't explain it with a simple analogy, explain it differently. Examples:
   - Encryption keys → padlock and key analogy
   - Hash functions → a meat grinder (one way, same input always same output, can't reverse it)
   - Public key crypto → a letterbox slot (anyone can post in, only you can open it)

3. **Core fundamentals before detail.** Always teach the "why does this exist / what problem does it solve" before explaining how it works. Syed's brain attaches new info to existing knowledge — so always build the hook first.

4. **Mix of three modes per topic:**
   - **Explain it** (teach clearly with analogy + example)
   - **Summarise it** (condensed notes he can keep)
   - **Test it** (scenario questions, "what's wrong with this system", quizzes)

5. **No walls of text.** Use headers, bullet points, tables, and clear structure. Dense paragraphs are hard to absorb.

---

## The Learning System (Overview)

Each module follows a 3-phase cycle:

### Phase 1 — Ingestion
- Claude reads all raw module materials (PDFs, slides)
- Claude distills the content into a clean, structured lesson
- Claude teaches it using the learning style above
- No need for Syed to read raw slides — Claude does that work

### Phase 2 — Active Recall
- Syed closes all notes
- Syed writes from memory what he can recall
- Claude reviews what was missed and fills gaps
- This is the most important phase — do not skip it

### Phase 3 — Testing
- Claude creates scenario-based questions (like real exam questions)
- Syed writes full answers
- Claude gives detailed feedback
- Repeat until confident

---

## The 6 Modules (to be filled in)

> When starting a new module session, update this section with the module name, code, folder path, and exam date if known.

| # | Module Name | Code | Folder Path | Status |
|---|-------------|------|-------------|--------|
| 1 | Implementing Secure Systems | WM242 | `/Users/syedimaduddin/Documents/ISS Module Materials (ALL)` | Ingested (June 2026) |
| 2 | TBD | — | — | Not started |
| 3 | TBD | — | — | Not started |
| 4 | TBD | — | — | Not started |
| 5 | TBD | — | — | Not started |
| 6 | TBD | — | — | Not started |

---

## Obsidian / Zettelkasten Integration

All notes produced in sessions should be formatted for Obsidian:

- Use `[[WikiLinks]]` when referencing concepts that exist (or should exist) as their own note
- Use tags at the bottom of each note: `#module/ISS`, `#topic/cryptography`, `#status/reviewed`
- Each atomic concept = one note (Zettelkasten principle)
- Notes should have: a one-line definition, an analogy, key points, links to related concepts

### Folder Structure (Obsidian Vault)
```
/Second Brain
  /00 - Index
  /01 - WM242 Implementing Secure Systems
  /02 - [Module 2]
  /03 - [Module 3]
  /04 - [Module 4]
  /05 - [Module 5]
  /06 - [Module 6]
  /Templates
  /MOC (Maps of Content)
```

---

## Session Protocol

When Syed starts a new session, he will say something like:
- "Let's do [Module Name]" — start Phase 1
- "Quiz me on [topic]" — jump to Phase 3
- "I want to review [topic]" — re-teach a specific concept
- "Continue where we left off" — check status in this file and resume

Always confirm at the start of a session:
1. What module/topic we're covering
2. Which phase we're in
3. What was last covered (check this file)

---

## Progress Log

> Update this after every session.

| Date | Module | Phase | Topics Covered | Notes |
|------|--------|-------|----------------|-------|
| June 2026 | WM242 ISS | 1 (Ingestion) | All 15 weeks — Weeks 1,2,3,4,5,7,8,9,10,11,12,13,14,15,17,19 | Full guide created. Practice exam analysed. |

---

## Important Notes for Claude

- Do NOT hallucinate. Every fact you teach must come from the actual module materials. If you are unsure, say so.
- Do NOT skip the analogy/visualisation step. Syed's learning style depends on it.
- Do NOT dump everything at once. Teach one topic at a time, confirm understanding, then move on.
- DO flag if a concept in a new module connects to something already learned — cross-linking is key to Zettelkasten.
- DO be honest about complexity. Some topics are genuinely hard. Say so and go slower.
