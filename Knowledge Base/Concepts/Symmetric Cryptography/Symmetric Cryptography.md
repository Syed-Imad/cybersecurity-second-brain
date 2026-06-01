# Symmetric Cryptography

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/symmetric #status/reviewed

---

## What is it?
Encryption where the same single key is used to both encrypt and decrypt.

## The Analogy
A padlock where the same key locks and unlocks it. Both people need a copy of the same key — which means you first need to safely hand over a copy.

## Key Properties
| Property | Detail |
|----------|--------|
| Keys | One shared secret key |
| Speed | Fast — good for large volumes of data |
| Use case | Encrypting data at rest, bulk data transfer |
| Weakness | Key distribution problem — how do you share the key securely? |
| No non-repudiation | Can't prove *which* party sent a message |

## Block vs Stream Ciphers

| | Block Cipher | Stream Cipher |
|--|-------------|--------------|
| Operates on | Fixed-size blocks (64 or 128 bits) | One bit or byte at a time |
| Examples | AES, DES | RC4 |
| Use case | Files, data at rest | Real-time comms, video |

## Connected concepts
- [[AES Advanced Encryption Standard]] — current standard
- [[DES Data Encryption Standard]] — old, now broken
- [[Modes of Operation]] — how to apply block ciphers to variable-length data
- [[Asymmetric Cryptography]] — solves the key distribution problem

---
*Source: WM242 Week 2 | Last reviewed: June 2026*
