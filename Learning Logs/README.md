# Learning Logs

A record of every learning session — what was covered, what clicked, what didn't, and where to pick up next time.

---

## Why This Exists

Without logs:
- Every session starts cold — Claude has no memory of what you've done
- Things that worked well (a great analogy, a useful question format) get lost
- You can't see your own patterns — which topics you always struggle with
- You can't continue a session days later without losing context

With logs:
- Start any session with: `"Read CLAUDE.md and my last log in Learning Logs/"` and Claude picks up exactly where you left off
- Query patterns: `"Read all my Learning Logs and tell me which topics I've struggled with most"`
- Build a record of your growth over time
- Flag things that were genuinely useful so they're not forgotten

---

## How to Start a Session Using a Log

```
Read CLAUDE.md and Learning Logs/[most recent log].
Continue from where we left off.
```

Or to query across all logs:
```
Read all files in Learning Logs/ and tell me:
- Which topics have I covered?
- Which ones did I struggle with?
- What's been left incomplete?
- Where should I start today?
```

---

## Log Naming Convention

```
YYYY-MM-DD — [Module] — [Phase] — [Topic].md
```

Examples:
```
2026-06-01 — WM242 — Phase 1 — Full Ingestion.md
2026-06-03 — WM242 — Phase 2 — Active Recall Hashing.md
2026-06-10 — WM242 — Phase 3 — Scenario Testing.md
2026-06-15 — TryHackMe — Rooms — Intro to Cryptography.md
```

---

## All Logs

| Date | Module | Phase | Topics | Outcome |
|------|--------|-------|--------|---------|
| 2026-06-01 | WM242 ISS | Phase 1 | Full module — all 16 weeks | Complete |

---

## Generating a Log

At the end of any session, ask Claude:
```
Write a learning log for this session and save it to
Learning Logs/[date] — [module] — [phase] — [topic].md
```

Claude will fill in the template below automatically.
