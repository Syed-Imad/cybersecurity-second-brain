# AES — Advanced Encryption Standard

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/symmetric #status/reviewed

---

## What is it?
The current global standard for symmetric encryption. Used in HTTPS, VPNs, file encryption, and almost everything secure today.

## The Analogy
A sophisticated bank vault that scrambles your valuables through 10–14 layers of locks, each using a different sub-key. Even if an attacker knows every lock's design, without the master key they'd need billions of years to brute force it.

## Key Facts
| Property | Value |
|----------|-------|
| Developed by | Vincent Rijmen & Joan Daemen (Rijndael) |
| Standardised | 2000 by NIST |
| Key sizes | 128, 192, or 256 bits |
| Block size | 128 bits (16 bytes in a 4×4 matrix) |
| Structure | Substitution-permutation network (NOT Feistel) |
| Rounds | 10 (128-bit), 12 (192-bit), 14 (256-bit) |

## The Round Operations (memorise these)
Each main round applies four operations in order:

| Step | What it does |
|------|-------------|
| **SubBytes** | Replace each byte using a lookup table (S-box) — adds confusion |
| **ShiftRows** | Shift rows of the 4×4 matrix left by 0,1,2,3 positions — adds diffusion |
| **MixColumns** | Multiply each column mathematically — spreads influence across bytes |
| **AddRoundKey** | XOR the block with the round sub-key — applies the actual key |

## The Three Round Types
- **Initial round:** AddRoundKey only
- **Main rounds:** SubBytes → ShiftRows → MixColumns → AddRoundKey
- **Final round:** SubBytes → ShiftRows → AddRoundKey ← **MixColumns is skipped**

> Exam tip: The one thing that's different in the final round is MixColumns is omitted.

## For 128-bit key: 2¹²⁸ possible keys = 340 undecillion combinations. Unbreakable by brute force.

## Connected concepts
- [[DES Data Encryption Standard]] — what AES replaced
- [[Modes of Operation]] — AES needs a mode to handle variable-length messages
- [[Symmetric Cryptography]]
- [[Shannon Confusion and Diffusion]] — SubBytes = confusion, ShiftRows/MixColumns = diffusion

---
*Source: WM242 Week 2 | Last reviewed: June 2026*
