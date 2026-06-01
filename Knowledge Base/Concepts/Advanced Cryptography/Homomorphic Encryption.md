# Homomorphic Encryption

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/advanced-crypto #status/reviewed

---

## What is it?
Encryption that allows computations to be performed on encrypted data without ever decrypting it. The result, when decrypted, matches what you'd get computing on the original plaintext.

## The Analogy
A locked transparent glove box in a lab. Scientists can put their hands through built-in gloves and manipulate the samples inside — mix, measure, process — without ever opening the box or touching the sample directly. Only the person with the key can open the box and take out the result.

## Why It Matters
Cloud computing problem: you want Google to run analysis on your medical data, but you don't trust Google with your data. With FHE: Google computes on ciphertext, returns ciphertext result, only you can decrypt it. Google never sees your data.

## PHE vs FHE
| | Partial (PHE) | Full (FHE) |
|--|--------------|-----------|
| Operations | One type only, unlimited times | Both + and × unlimited times |
| Example | RSA (multiplication), Paillier (addition) | BGV, BFV, CKKS |
| Speed | Fast | ~1 million× slower than plaintext |
| Practical today | ✅ Yes | ⚠️ Limited use cases |

## FHE Schemes (all lattice-based, quantum-safe)
| Scheme | Works on |
|--------|---------|
| **BGV** | Integers |
| **BFV** | Integers |
| **CKKS** | Complex/approximate numbers |

## The Noise Problem
A small random "noise" is added to ciphertext for security. Each operation increases noise. Too much noise → decryption fails. Managing noise is the central engineering challenge of FHE.

## Connected concepts
- [[RSA]] — partially homomorphic (multiplication)
- [[Lattice-Based Cryptography]]
- [[Post-Quantum Cryptography]] — FHE schemes are quantum-safe

---
*Source: WM242 Week 14 | Last reviewed: June 2026*
