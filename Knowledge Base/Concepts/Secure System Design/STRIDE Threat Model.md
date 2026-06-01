# STRIDE Threat Model

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/system-design #status/reviewed

---

## What is it?
A structured framework for identifying security threats during system design. Each letter is a category of threat.

## The Analogy
A checklist a security guard runs through before a building opens: Could someone pretend to be staff? Could someone tamper with records? Could someone deny doing something they did? Could someone leak data? Could someone crash the system? Could someone gain more power than they should have?

## STRIDE Breakdown

| Letter | Threat | CIA Pillar violated | Example |
|--------|--------|--------------------|---------| 
| **S** | Spoofing | Authentication | Attacker pretends to be a legitimate user |
| **T** | Tampering | Integrity | Attacker modifies data in transit |
| **R** | Repudiation | Non-repudiation | User denies performing a transaction |
| **I** | Information Disclosure | Confidentiality | Data exposed to unauthorised parties |
| **D** | Denial of Service | Availability | System flooded until it crashes |
| **E** | Elevation of Privilege | Authorisation | Normal user gains admin access |

## How to Use It
For each component of your system, ask: can any of these 6 things happen here? If yes — design a mitigation.

## Connected concepts
- [[8 Principles of Secure System Design]]
- [[CIA Triad]]
- [[Secure SDLC]]

---
*Source: WM242 Week 8 | Last reviewed: June 2026*
