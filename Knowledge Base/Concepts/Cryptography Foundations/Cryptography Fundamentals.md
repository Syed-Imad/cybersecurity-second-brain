# Cryptography Fundamentals

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/foundations #status/reviewed

---

## What is it?
The science of securing information by transforming it into an unreadable format so only intended parties can access it.

## The Analogy
Passing a note in class written in a secret code only your friend understands. Even if the teacher intercepts it, they can't read it.

## The 9 Core Concepts
| Concept | What it means |
|---------|--------------|
| **Confidentiality** | Only authorised parties can read the data |
| **Integrity** | Data hasn't been altered |
| **Authenticity** | You can verify who sent the message |
| **Non-Repudiation** | The sender can't deny sending it |
| **Trust** | Confidence the system works as expected |
| **Secrets & Keys** | The critical elements that make crypto work |
| **Identity** | Establishing who is communicating |
| **Certificates** | Digital documents that verify identities |
| **Randomness & Entropy** | Unpredictability that prevents guessing |

## Shannon's Two Principles
- **Confusion** — make the relationship between ciphertext and key as complex as possible
- **Diffusion** — spread the influence of each plaintext character across the whole ciphertext
> Used in AES today.

## Connected concepts
- [[CIA Triad]] — the three security goals crypto protects
- [[AES Advanced Encryption Standard]] — confusion + diffusion in action
- [[Entropy and Randomness]]
- [[Caesar Cipher]] — the simplest example of a cipher

---
*Source: WM242 Week 1 | Last reviewed: June 2026*
