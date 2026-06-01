# CIA Triad

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/foundations #status/reviewed

---

## What is it?
The three core goals of any secure system: Confidentiality, Integrity, Availability.

## The Analogy
Think of a bank vault:
- **Confidentiality** — only the account holder can see what's inside
- **Integrity** — nobody can tamper with the contents without it being noticed
- **Availability** — the vault opens when you need it, not just sometimes

## The Three Pillars

| Pillar | Meaning | Broken by |
|--------|---------|-----------|
| **Confidentiality** | Only authorised parties can read the data | Eavesdropping, data leaks |
| **Integrity** | Data is unaltered during storage or transit | Tampering, man-in-the-middle |
| **Availability** | Data and systems are accessible when needed | DDoS, hardware failure |

## Why it matters
Every security decision maps back to one or more of these three.
When a system is compromised, you ask: which pillar failed?

## Connected concepts
- [[Cryptography Fundamentals]] — crypto protects all three pillars
- [[STRIDE Threat Model]] — each STRIDE threat maps to a CIA violation
- [[Hashing]] — protects integrity
- [[Encryption]] — protects confidentiality

---
*Source: WM242 Week 1 | Last reviewed: June 2026*
