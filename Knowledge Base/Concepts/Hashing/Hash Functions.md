# Hash Functions

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/hashing #status/reviewed

---

## What is it?
A one-way mathematical function that takes any input and produces a fixed-length fingerprint (the hash). Cannot be reversed.

## The Analogy
A meat grinder. You can put any amount of raw meat in and always get the same type of minced output. Put the same steak in twice → identical mince. Put a slightly different steak in → completely different mince. And you can never reconstruct the original steak from the mince.

## Key Properties
| Property | Meaning |
|----------|---------|
| **Variable input** | Any length of input accepted |
| **Fixed output** | Always produces the same length output |
| **Deterministic** | Same input → always same output |
| **One-way** | Cannot reverse the hash to get the input |
| **Avalanche effect** | One bit change in input → completely different output |
| **Collision resistant** | Near-impossible to find two inputs with the same hash |

## The Algorithms

| Algorithm | Output size | Status |
|-----------|------------|--------|
| MD5 | 128-bit | ❌ Broken — do not use |
| SHA-1 | 160-bit | ❌ Deprecated — do not use |
| SHA-256 | 256-bit | ✅ Current standard |
| SHA-512 | 512-bit | ✅ Current standard |
| SHA-3 | Variable | ✅ Next-gen |
| Argon2 | Variable | ✅ Best for passwords |

## Where Hashes Are Used
- **Password storage** — store the hash, never the password
- **Data integrity** — hash a file before and after transfer; if hashes match, nothing changed
- **Digital signatures** — sign the hash of a document, not the whole document
- **Blockchain** — each block contains the hash of the previous block

## Connected concepts
- [[Preimage Resistance]]
- [[Collision Resistance]]
- [[Salting]]
- [[HMAC]]
- [[Digital Signatures]]

---
*Source: WM242 Week 3 | Last reviewed: June 2026*
