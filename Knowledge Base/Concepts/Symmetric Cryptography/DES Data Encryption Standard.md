# DES — Data Encryption Standard

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/symmetric #status/reviewed

---

## What is it?
The first widely adopted symmetric encryption standard. Now obsolete — replaced by AES.

## Key Facts
| Property | Value |
|----------|-------|
| Developed by | IBM, early 1970s |
| US Standard until | 2001 |
| Key size | **56 bits** (too small — this is why it's broken) |
| Block size | 64 bits |
| Structure | **Feistel Network** |
| Rounds | 16 |

## Why It's Broken
56-bit key = only 2⁵⁶ possible keys = ~72 quadrillion. Sounds huge but a modern computer can brute-force this in hours.

## Feistel Network (how DES works)
Each round:
1. Split block into Left (L) and Right (R) halves
2. Apply function f to R using the round sub-key
3. XOR the result with L
4. Swap halves → new L = old R, new R = XOR result
5. Repeat 16 times

## DES Round Steps
Key Generation → Initial Permutation → 16 Feistel rounds → Final Permutation

## Connected concepts
- [[AES Advanced Encryption Standard]] — what replaced DES
- [[Symmetric Cryptography]]
- [[Cryptanalysis Types]] — differential cryptanalysis was developed specifically to attack DES

---
*Source: WM242 Week 2 | Last reviewed: June 2026*
